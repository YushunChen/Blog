---
description: 'ID: 88; medium'
---

# Lowest Common Ancestor of a Binary Tree

{% embed url="https://www.lintcode.com/problem/88/" %}

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
    /*
     * @param root: The root of the binary search tree.
     * @param A: A TreeNode in a Binary.
     * @param B: A TreeNode in a Binary.
     * @return: Return the least common ancestor(LCA) of the two nodes.
     */
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode A, TreeNode B) {
        if (root == null)
            return null;
        if (root == A || root == B)
            return root;

        TreeNode left = lowestCommonAncestor(root.left, A, B);
        TreeNode right = lowestCommonAncestor(root.right, A, B);
        if (left != null && right != null)
            return root;
        if (left != null)
            return left;
        if (right != null)
            return right;
        
        return null;
    }
}
```

### Notes

There are 4 general cases.

1. If `root` is `A` or `B`, we directly return the root since both `A` and `B` are guaranteed to be in the tree. If the `root` is one of them, then the other one must be its descendent.
2. If `A` and `B` are on the different sides of the `root`, then the `root` of the LCA.
3. If `A` and `B` are both in the left tree, then we find the LCA of the left tree.
4. If `A` and `B` are both in the right tree, then we find the LCA of the right tree.



