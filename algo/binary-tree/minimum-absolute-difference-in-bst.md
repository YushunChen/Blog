---
description: ID: 530; easy
---
# Minimum Absolute Difference in BST

{% embed url="https://leetcode.com/problems/minimum-absolute-difference-in-bst/" %}

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

func getMinimumDifference(root *TreeNode) int {
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
Keep track of the previous node. Similar to an inorder traversal.
{% endhint %}
