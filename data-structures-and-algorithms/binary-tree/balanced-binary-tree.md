---
description: 'ID: 110; easy'
---

# Balanced Binary Tree

{% embed url="https://leetcode.com/problems/balanced-binary-tree/" %}

{% embed url="https://www.lintcode.com/problem/93/" %}

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

func isBalanced(root *TreeNode) bool {
    if root == nil {
        return true
    }
    leftDepth := depthHelper(root.Left)
    rightDepth := depthHelper(root.Right)
    if abs(leftDepth - rightDepth) > 1 {
        return false
    }
    return isBalanced(root.Left) && isBalanced(root.Right)
}

func depthHelper(root *TreeNode) int {
    if root == nil {
        return 0
    } 
    return max(depthHelper(root.Left), depthHelper(root.Right)) + 1
}

func max(x, y int) int {
    if x > y {
        return x
    }
    return y
}

func abs(x int) int {
    if x >= 0 {
        return x
    }
    return -x
}
```

## Solution 2 \(Java\)

```java

```

