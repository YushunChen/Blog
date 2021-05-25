---
description: 'ID: 94; easy'
---

# Binary Tree Inorder Traversal

{% embed url="https://leetcode.com/problems/binary-tree-inorder-traversal/" %}

## Solution 1

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func inorderTraversal(root *TreeNode) []int {
    result := make([]int, 0)
    inorderHelper(root, &result)
    return result
}

func inorderHelper(root *TreeNode, res *[]int) {
    if root != nil {
        inorderHelper(root.Left, res)
        *res = append(*res, root.Val)
        inorderHelper(root.Right, res)
    }
}
```

