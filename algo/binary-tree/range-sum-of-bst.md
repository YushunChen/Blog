---
description: ID: 938; easy
---
# Range Sum of BST

{% embed url="https://leetcode.com/problems/range-sum-of-bst/" %}

## Solution 1 (Java)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int rangeSumBST(TreeNode root, int low, int high) {
        int[] sum = new int[1];
        traverse(root, low, high, sum);
        return sum[0];
    }
    
    private void traverse(TreeNode root, int low, int high, int[] sum) {
        if (root == null) return;
        if (root.val >= low && root.val <= high)
            sum[0] += root.val;
        if (root.val > low)
            traverse(root.left, low, high, sum);
        if (root.val < high)
            traverse(root.right, low, high, sum);
    }
}
```

### Notes

* We utilize the condition that the tree is a BST. Note that you can use a normal traversal to traverse all the nodes, but it is not necessary to visit some nodes.
* If `root.val` is already less than or equal to `low` (less than `high` of course), we only traverse its right subtree. If `root.val` is already larger than or equal to `high` (more than `low`), we only traverse its left subtree.
