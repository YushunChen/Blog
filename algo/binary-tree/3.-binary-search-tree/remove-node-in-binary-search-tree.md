---
description: ID: 87; hard; 删除二叉查找树的节点
---
# Remove Node in Binary Search Tree

{% embed url="https://www.lintcode.com/problem/87/" %}

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
    /*
     * @param root: The root of the binary search tree.
     * @param value: Remove the node with given value.
     * @return: The root of the binary search tree after removal.
     */
    public TreeNode removeNode(TreeNode root, int value) {
        if (root == null)
            return root;
        if (value < root.val) {
            root.left = removeNode(root.left, value);
        } else if (value > root.val) {
            root.right = removeNode(root.right, value);
        } else {
            if (root.left == null && root.right == null)
                return null;
            if (root.left == null)
                return root.right;
            if (root.right == null)
                return root.left;
            
            int predecessor = findPred(root.left);
            root.val = predecessor;
            root.left = removeNode(root.left, predecessor);
        }
        return root;
    }

    private int findPred(TreeNode root) {
        if (root.right == null) 
            return root.val;
        return findPred(root.right);
    }
}
```

### Notes

First, we use the property of the binary search tree to find the value-matching node. If we find that node, then we have 4 cases:

1. The node is a leaf node. We can directly delete it.
2. The node has one right child, we delete it by returning its right child.
3. The node has one left child, we delete it by returning its left child.
4. The node has two children. We find its predecessor node, which is the node that has the maximum value that is less than the node's value. We replace the node with its predecessor and remove the old position of its predecessor. Here, we can also use successor, which is the node that has the minimum value that is larger then the nodes' value.

