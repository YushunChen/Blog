---
description: 'ID: 72; medium; 中序遍历和后序遍历树构造二叉树'
---

# Construct Binary Tree from Inorder and Postorder Traversal

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
     * @param inorder: A list of integers that inorder traversal of a tree
     * @param postorder: A list of integers that postorder traversal of a tree
     * @return: Root of a tree
     */
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        int inLen = inorder.length;
        int postLen = postorder.length;
        if (inLen == 0 || postLen == 0 || inLen != postLen)
            return null;
        
        int rootVal = postorder[postLen - 1];
        int index = 0;
        for (int i = 0; i < inorder.length; i++) {
            if (inorder[i] == rootVal) {
                index = i;
                break;
            }
        }
        TreeNode root = new TreeNode(rootVal);

        int[] leftNewInorder = Arrays.copyOfRange(inorder, 0, index);
        // left new post order has the same range as above
        int[] leftNewPostorder = Arrays.copyOfRange(postorder, 0, index);
        int[] rightNewInorder = Arrays.copyOfRange(inorder, index + 1, inLen);
        // right new post order excludes the last element (root)
        int[] rightNewPostorder = Arrays.copyOfRange(postorder, index, postLen - 1);

        TreeNode left = buildTree(leftNewInorder, leftNewPostorder);
        TreeNode right = buildTree(rightNewInorder, rightNewPostorder);
        root.left = left;
        root.right = right;
        return root;
    }
}
```

### Notes

1. Find the root of the tree. It should be the last element of the `postorder` array.
2. Find the index of the root in the `inorder` array.
3. The interval \[0, index\) of the `inorder` array contains the left subtree, and the interval \[index + 1, inLen\) of the `inorder` array contains the right subtree. 

