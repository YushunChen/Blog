---
description: ID: 783; easy
---
# Minimum Distance Between BST Nodes

{% embed url="https://leetcode.com/problems/minimum-distance-between-bst-nodes/" %}

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

import "math"

func minDiffInBST(root *TreeNode) int {
    result, previous := math.MaxInt16, -1
    getMinDiffHelper(root, &result, &previous)
    return result
}

func getMinDiffHelper(root *TreeNode, res, prev *int) {
    if root == nil {
        return
    }
    getMinDiffHelper(root.Left, res, prev)
    if *prev != -1 {
        *res = min(*res, abs(root.Val - *prev))
    }
    *prev = root.Val
    getMinDiffHelper(root.Right, res, prev)
}

func min(x, y int) int {
    if x > y {
        return y
    }
    return x
}

func abs(x int) int {
    if x >= 0 {
        return x
    }
    return -x
}
```

{% hint style="info" %}
Exactly the same as ID: 530.
{% endhint %}
