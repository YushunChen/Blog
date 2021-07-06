---
description: 'ID: 482; easy; 二叉树的某层节点之和'
---

# Binary Tree Level Sum

{% embed url="https://www.lintcode.com/problem/482/" %}

## Solution 1 \(Java\)

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */

public class Solution {
    /**
     * @param root: the root of the binary tree
     * @param level: the depth of the target level
     * @return: An integer
     */
    public int levelSum(TreeNode root, int level) {
        int sum = 0;
        if (root == null || level == 0) return sum;
        return bfs(root, sum, level);
    }

    private int bfs(TreeNode root, int sum, int level) {
        List<Integer> result = new ArrayList<>();
        result.add(root.val);
        Queue<TreeNode> q = new ArrayDeque<>();
        q.offer(root);
        while (level > 1 && !q.isEmpty()) {
            int size = q.size();
            int levelSum = 0;
            for (int i = 0; i < size; i++) {
                TreeNode curr = q.poll();
                if (curr.left != null) {
                    levelSum += curr.left.val;
                    q.offer(curr.left);
                }
                if (curr.right != null) {
                    levelSum += curr.right.val;
                    q.offer(curr.right);
                }
            }
            result.add(levelSum);
            level--;
        }
        return result.get(result.size() - 1);
    }
}
```

### Notes

* BFS

## Solution 2 \(Java\)

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */

public class Solution {
    /**
     * @param root: the root of the binary tree
     * @param level: the depth of the target level
     * @return: An integer
     */
    public int levelSum(TreeNode root, int level) {
        int sum = 0;
        if (root == null || level == 0) return sum;
        return bfs(root, sum, level);
    }

    private int bfs(TreeNode root, int sum, int level) {
        Queue<TreeNode> q = new ArrayDeque<>();
        q.offer(root);
        while (!q.isEmpty()) {
            int size = q.size();
            int levelSum = 0;
            level--;
            for (int i = 0; i < size; i++) {
                TreeNode curr = q.poll();
                if (level == 0)
                    levelSum += curr.val;
                if (curr.left != null)
                    q.offer(curr.left);
                if (curr.right != null)
                    q.offer(curr.right);
            }
            if (level == 0) return levelSum;
        }
        return sum;
    }
}
```

### Notes

* Optimized BFS

