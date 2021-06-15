---
description: 'ID: 104; easy'
---

# TODO: Maximum Depth of Binary Tree

{% embed url="https://leetcode.com/problems/maximum-depth-of-binary-tree/" %}

{% embed url="https://www.lintcode.com/problem/97/" %}

## Solution 1 \(Golang\)

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func maxDepth(root *TreeNode) int {
    if root == nil {
        return 0
    }
    return max(maxDepth(root.Left), maxDepth(root.Right)) + 1
}

func max(x, y int) int {
    if x > y {
        return x
    }
    return y
}
```

## Solution 2 \(Java\)

```java

```

