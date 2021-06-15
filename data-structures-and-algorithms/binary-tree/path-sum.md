---
description: 'ID: 112; easy'
---

# Path Sum

{% embed url="https://leetcode.com/problems/path-sum/" %}

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
func hasPathSum(root *TreeNode, targetSum int) bool {
    if root == nil {
        return false
    }
    if root.Left == nil && root.Right == nil {
        return root.Val == targetSum
    }
    curVal := targetSum - root.Val
    return hasPathSum(root.Left, curVal) || hasPathSum(root.Right, curVal)
}
```

