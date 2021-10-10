---
description: ID: 578; medium
---
# Lowest Common Ancestor III

{% embed url="https://www.lintcode.com/problem/578/" %}

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

    private class Result {
        public boolean hasA, hasB;
        public Result(boolean hasA, boolean hasB) {
            this.hasA = hasA;
            this.hasB = hasB;
        }
    }

    private TreeNode res = null;

    /*
     * @param root: The root of the binary tree.
     * @param A: A TreeNode
     * @param B: A TreeNode
     * @return: Return the LCA of the two nodes.
     */
    public TreeNode lowestCommonAncestor3(TreeNode root, TreeNode A, TreeNode B) {
        dfs(root, A, B);
        return res;
    }

    private Result dfs(TreeNode root, TreeNode A, TreeNode B) {
        if (root == null)
            return new Result(false, false);
        
        Result left = dfs(root.left, A, B);
        Result right = dfs(root.right, A, B);

        boolean a = left.hasA || right.hasA || root == A;
        boolean b = left.hasB || right.hasB || root == B;

        if (a && b && res == null)
            res = root;

        return new Result(a, b);
    }
}
```

### Notes

* We use the `Result` class to keep track of the status of `A` and `B` in the tree.
* If `a` and `b` are both `true`, which means the current `root` is already is LCA, then we set `res` only when it is null. This if statement is `true` for the LCA and its ancestors, but we are guaranteed to have the LCA. The reason is that we are doing a DFS and the LCA appears first. Once we set `res` to the LCA, we do not update it and do not care about its ancestors.
