---
description: ID: 98; medium; 验证二叉查找树
---
# Validate Binary Search Tree

{% embed url="https://leetcode.com/problems/validate-binary-search-tree/" %}

{% embed url="https://www.lintcode.com/problem/95/" %}

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
     * @param root: The root of binary tree.
     * @return: True if the binary tree is BST, or false
     */
    public boolean isValidBST(TreeNode root) {
        return isValidBSTHelper(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean isValidBSTHelper(TreeNode root, long min, long max) {
        if (root == null)
            return true;
        if (root.val <= min || root.val >= max)
            return false;
        boolean isLeftValid = isValidBSTHelper(root.left, min, root.val);
        boolean isRightValid = isValidBSTHelper(root.right, root.val, max);
        return isLeftValid && isRightValid;
    }
}
```
