---
description: ID: 94; medium
---
# Binary Tree Maximum Path Sum

{% embed url="https://www.lintcode.com/problem/94/" %}

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

    private int maxPathSum = Integer.MIN_VALUE;

    /**
     * @param root: The root of binary tree.
     * @return: An integer
     */
    public int maxPathSum(TreeNode root) {
        dfs(root);
        return maxPathSum;
    }

    private int dfs(TreeNode root) {
        if (root == null)
            return 0;
        
        int left = dfs(root.left);
        int right = dfs(root.right);

        maxPathSum = Math.max(maxPathSum, left + root.val);
        maxPathSum = Math.max(maxPathSum, right + root.val);
        maxPathSum = Math.max(maxPathSum, root.val);
        maxPathSum = Math.max(maxPathSum, left + right + root.val);

        return Math.max(Math.max(left, right), 0) + root.val;
    }
}
```

### Notes

There are 4 types of paths that can be candidates for the maximum path sum.

1. Max path of left tree + root
2. Max path of right tree + root
3. Only the root
4. Max single path of left tree + root + max single path of right tree

