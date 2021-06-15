---
description: 'ID: 257; easy'
---

# Binary Tree Paths

{% embed url="https://leetcode.com/problems/binary-tree-paths/" %}

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

import "strconv"

func binaryTreePaths(root *TreeNode) []string {
    if root == nil {
        return []string{}
    }
    if root.Left == nil && root.Right == nil {
        return []string{strconv.Itoa(root.Val)}
    }
    result := make([]string, 0)
    leftPaths := binaryTreePaths(root.Left)
    for _,lp := range leftPaths {
        result = append(result, strconv.Itoa(root.Val) + "->" + lp)
    }
    rightPaths := binaryTreePaths(root.Right)
    for _,rp := range rightPaths {
        result = append(result, strconv.Itoa(root.Val) + "->" + rp)
    }
    return result
}
```

