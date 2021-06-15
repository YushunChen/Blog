---
description: 'ID: 226; easy'
---

# Invert Binary Tree

{% embed url="https://leetcode.com/problems/invert-binary-tree/" %}

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
func invertTree(root *TreeNode) *TreeNode {
    if root == nil {
        return nil
    }
    invertTree(root.Left)
    invertTree(root.Right)
    root.Left, root.Right = root.Right, root.Left
    return root
}
```

