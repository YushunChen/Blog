---
description: ID: 1115; easy; 二叉树每层的平均数
---
# Average of Levels in Binary Tree

{% embed url="https://www.lintcode.com/problem/1115/" %}

## Solution 1 (Java)

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
     * @param root: the binary tree of the  root
     * @return: return a list of double
     */
    public List<Double> averageOfLevels(TreeNode root) {
        if (root == null) return null;
        List<Double> res = new ArrayList<Double>();
        Queue<TreeNode> q = new ArrayDeque<TreeNode>();
        q.offer(root);

        while (!q.isEmpty()) {
            int size = q.size();
            double sum = 0;
            for (int i = 0; i < size; i++) {
                TreeNode node = q.poll();
                sum += node.val;
                if (node.left != null)
                    q.offer(node.left);
                if (node.right != null)
                    q.offer(node.right);
            }
            res.add(sum / size);
        }
        return res;
    }
}
```

### Notes

* BFS
