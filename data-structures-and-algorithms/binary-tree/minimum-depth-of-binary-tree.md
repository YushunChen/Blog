---
description: 'ID: 111; easy'
---

# Minimum Depth of Binary Tree

{% embed url="https://leetcode.com/problems/minimum-depth-of-binary-tree/" %}

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
func minDepth(root *TreeNode) int {
    if root == nil {
        return 0
    }
    if root.Right == nil {
        return minDepth(root.Left) + 1
    }
    if root.Left == nil {
        return minDepth(root.Right) + 1
    }
    return min(minDepth(root.Left), minDepth(root.Right)) + 1
}

func min(x, y int) int {
    if x < y {
        return x
    }
    return y
}
```

