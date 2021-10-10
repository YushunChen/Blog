---
description: ID: 448; medium; 二叉查找树的中序后继
---
# Inorder Successor in BST

{% embed url="https://www.lintcode.com/problem/448/" %}

## Solution 1 (Java)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */


public class Solution {

    TreeNode successor = null;

    /*
     * @param root: The root of the BST.
     * @param p: You need find the successor node of p.
     * @return: Successor of p.
     */
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        dfs(root, p);
        return successor;
    }

    private void dfs(TreeNode root, TreeNode p) {
        if (root == null || p == null)
            return;
        if (p.val >= root.val) {
            dfs(root.right, p);
        } else {
            successor = root;
            dfs(root.left, p);
        }
    }
}
```

### Notes

* Recursion

## Solution 2 (Java)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */


public class Solution {
    /*
     * @param root: The root of the BST.
     * @param p: You need find the successor node of p.
     * @return: Successor of p.
     */
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        TreeNode successor = null;
        while (root != null) {
            if (root.val > p.val) {
                successor = root;
                root = root.left;
            } else {
                root = root.right;
            }
        }
        return successor;
    }
}
```

### Notes

* Traversal
