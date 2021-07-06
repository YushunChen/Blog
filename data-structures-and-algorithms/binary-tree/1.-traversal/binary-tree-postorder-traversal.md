---
description: 'ID: 145; easy'
---

# Binary Tree Postorder Traversal

{% embed url="https://leetcode.com/problems/binary-tree-postorder-traversal/" %}

{% embed url="https://www.lintcode.com/problem/68/" %}

## Solution 1 \(Go\)

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func postorderTraversal(root *TreeNode) []int {
    res := make([]int, 0)
    postorderHelper(root, &res)
    return res
}

func postorderHelper(root *TreeNode, res *[]int) {
    if root != nil {
        postorderHelper(root.Left, res)
        postorderHelper(root.Right, res)
        *res = append(*res, root.Val)
    }
}
```

## Solution 2 \(Java\)

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
     * @param root: A Tree
     * @return: Postorder in ArrayList which contains node values.
     */
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        postorderTraversalHelper(root, result);
        return result;
    }

    private void postorderTraversalHelper(TreeNode root, List<Integer> result) {
        if (root == null) return;
        postorderTraversalHelper(root.left, result);
        postorderTraversalHelper(root.right, result);
        result.add(root.val);
    }
}
```

### Notes

* Recursion / Divide and conquer 

## Solution 3 \(Java\)

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
     * @param root: A Tree
     * @return: Postorder in ArrayList which contains node values.
     */
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Deque<TreeNode> stack = new ArrayDeque<>();
        if (root == null) return result;
        TreeNode curr = root;
        TreeNode prev = null;
        stack.push(root);

        while (!stack.isEmpty()) {
            curr = stack.peek();
            // traversal down the tree
            if (prev == null || prev.left == curr || prev.right == curr) {
                if (curr.left != null) {
                    stack.push(curr.left);
                } else if (curr.right != null) {
                    stack.push(curr.right);
                }
            } else if (curr.left == prev) {
                // if the left is visited, visit the right
                if (curr.right != null) {
                    stack.push(curr.right);
                }
            } else { // curr.right == prev
                // if the right is visited, visit the middle
                result.add(curr.val);
                stack.pop();
            }
            prev = curr;
        }

        return result;
    }
}
```

### Notes

* Traversal

