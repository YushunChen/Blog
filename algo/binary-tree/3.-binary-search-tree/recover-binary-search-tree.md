---
description: ID: 691; medium; 恢复二叉搜索树
---
# Recover Binary Search Tree

{% embed url="https://www.lintcode.com/problem/691/" %}

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
     * @param root: the given tree
     * @return: the tree after swapping
     */
    public TreeNode bstSwappedNode(TreeNode root) {
        // nodes inorder should be non-decreasing
        List<TreeNode> nodes = new ArrayList<>();
        inorderTraversal(root, nodes);

        TreeNode firstWrongNode = null, secondWrongNode = null;
        for (int i = 1; i < nodes.size(); i++) {
            if (nodes.get(i).val < nodes.get(i - 1).val) {
                if (firstWrongNode == null)
                    firstWrongNode = nodes.get(i - 1);
                secondWrongNode = nodes.get(i);
            }
        }

        if (firstWrongNode != null) {
            int temp = firstWrongNode.val;
            firstWrongNode.val = secondWrongNode.val;
            secondWrongNode.val = temp;
        }

        return root;
    }

    private void inorderTraversal(TreeNode root, List<TreeNode> nodes) {
        if (root == null)
            return;
        inorderTraversal(root.left, nodes);
        nodes.add(root);
        inorderTraversal(root.right, nodes);
    }
}
```

### Notes

* Use [inorder traversal](../1.-traversal/binary-tree-inorder-traversal.md) and put the nodes into a list.
* The list should be in non-decreasing order by construction. Iterate the list to find the node that is smaller than its previous node, then swap these two nodes.
* Space complexity is `O(n)`

## Solution 2 (Java)

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

    TreeNode first = null, second = null, prev = null;

    /**
     * @param root: the given tree
     * @return: the tree after swapping
     */
    public TreeNode bstSwappedNode(TreeNode root) {
        prev = new TreeNode(Integer.MIN_VALUE);
        inorderTraversal(root);

        if (first != null) {
            int temp = first.val;
            first.val = second.val;
            second.val = temp;
        }
        return root;
    }

    private void inorderTraversal(TreeNode root) {
        if (root == null)
            return;

        inorderTraversal(root.left);
        if (root.val < prev.val) {
            if (first == null)
                first = prev;
            second = root;
        }
        prev = root;
        inorderTraversal(root.right);
    }
}
```



### Notes

* We still use [inorder traversal](../1.-traversal/binary-tree-inorder-traversal.md) but modify it to check if we have any out-of-order nodes (the two nodes that are not in non-decreasing order).
* Space complexity is `O(1)`
