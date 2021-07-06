---
description: 'ID: 475; medium'
---

# Binary Tree Maximum Path Sum II

{% embed url="https://www.lintcode.com/problem/475/" %}

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
     * @param root: the root of binary tree.
     * @return: An integer
     */
    public int maxPathSum2(TreeNode root) {
        if (root == null)
            return 0;
        
        int leftSum = maxPathSum2(root.left);
        int rightSum = maxPathSum2(root.right);
        int leftOrRight = Math.max(leftSum + root.val, rightSum + root.val);
        return Math.max(root.val, leftOrRight);
    }
}
```

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

    private class SumNode {
        public TreeNode node;
        public int sum;
        public SumNode(TreeNode node, int sum) {
            this.node = node;
            this.sum = sum;
        }
    }

    /**
     * @param root: the root of binary tree.
     * @return: An integer
     */
    public int maxPathSum2(TreeNode root) {
        if (root == null)
            return 0;
        
        int ans = Integer.MIN_VALUE;
        Queue<SumNode> q = new ArrayDeque<>();
        q.offer(new SumNode(root, root.val));
        while (!q.isEmpty()) {
            SumNode curr = q.poll();
            if (curr.sum > ans)
                ans = curr.sum;
            if (curr.node.left != null)
                q.offer(new SumNode(curr.node.left, curr.sum + curr.node.left.val));
            if (curr.node.right != null)
                q.offer(new SumNode(curr.node.right, curr.sum + curr.node.right.val));
        }
        return ans;
    }
}
```

### Notes

* Non-recursive version using a queue.

