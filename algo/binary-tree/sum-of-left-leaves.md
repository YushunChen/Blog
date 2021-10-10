---
description: ID: 404; easy
---
# Sum of Left Leaves

{% embed url="https://leetcode.com/problems/sum-of-left-leaves/" %}

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
func sumOfLeftLeaves(root *TreeNode) int {
    if root == nil {
        return 0
    }
    if root.Left != nil && root.Left.Left == nil && root.Left.Right == nil {
        return root.Left.Val + sumOfLeftLeaves(root.Right)
    }
    return sumOfLeftLeaves(root.Left) + sumOfLeftLeaves(root.Right)
}
```
