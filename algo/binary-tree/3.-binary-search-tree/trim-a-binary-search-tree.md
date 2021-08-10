---
description: 'ID: 701; medium; 修剪二叉搜索树'
---

# Trim a Binary Search Tree

{% embed url="https://www.lintcode.com/problem/701/" %}

{% embed url="https://leetcode.com/problems/trim-a-binary-search-tree/" %}

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
     * @param root: given BST
     * @param minimum: the lower limit
     * @param maximum: the upper limit
     * @return: the root of the new tree 
     */
    public TreeNode trimBST(TreeNode root, int minimum, int maximum) {
        if (root == null)
            return null;

        if (root.val < minimum)
            return trimBST(root.right, minimum, maximum);
        if (root.val > maximum)
            return trimBST(root.left, minimum, maximum);

        root.left = trimBST(root.left, minimum, maximum);
        root.right = trimBST(root.right, minimum, maximum);
        return root;
    }
}
```

