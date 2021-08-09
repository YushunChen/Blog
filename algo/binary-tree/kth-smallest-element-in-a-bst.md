---
description: 'ID: 230; medium'
---

# Kth Smallest Element in a BST

{% embed url="https://leetcode.com/problems/kth-smallest-element-in-a-bst/" %}

## Solution 1 \(Java\)

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
    public int kthSmallest(TreeNode root, int k) {
        Deque<TreeNode> stack = new ArrayDeque<>();
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
        
        for (int i = 0; i < k - 1; i++) {
            TreeNode curr = stack.peek();
            if (curr.right == null) {
                curr = stack.pop();
                while (!stack.isEmpty() && stack.peek().right == curr) {
                    curr = stack.pop();
                }
            } else {
                curr = curr.right;
                while (curr != null) {
                    stack.push(curr);
                    curr = curr.left;
                }
            }
        }
        
        return stack.peek().val;
    }
}
```

### Notes

* This solution is similar to [Binary Search Tree Iterator](3.-binary-search-tree/binary-search-tree-iterator.md).

