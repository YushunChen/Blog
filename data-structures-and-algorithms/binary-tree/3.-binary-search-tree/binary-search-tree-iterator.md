---
description: 'ID: 86; hard; 二叉查找树迭代器'
---

# Binary Search Tree Iterator

{% embed url="https://www.lintcode.com/problem/86/" %}

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
 * Example of iterate a tree:
 * BSTIterator iterator = new BSTIterator(root);
 * while (iterator.hasNext()) {
 *    TreeNode node = iterator.next();
 *    do something for node
 * } 
 */


public class BSTIterator {

    private Deque<TreeNode> stack;
    private TreeNode next;
    /**
    * @param root: The root of binary tree.
    */
    public BSTIterator(TreeNode root) {
        stack = new ArrayDeque<TreeNode>();
        next = root;
    }

    /**
     * @return: True if there has next node, or false
     */
    public boolean hasNext() {
        if (next != null) {
            TreeNode curr = next;
            while (curr != null) {
                stack.push(curr);
                curr = curr.left;
            }
            next = null;
        }
        return !stack.isEmpty();
    }

    /**
     * @return: return next node
     */
    public TreeNode next() {
        if (!hasNext())
            return null;
        TreeNode curr = stack.pop();
        next = curr.right;
        return curr;
    }
}
```

### Notes

* Use stack to store all the left children. 
* If the stack is empty, then there is no next node.
* The top of the stack is the current node. In terms of the tree structure, the next node of the current node is its right child.

