---
description: ID: 235; easy
---
# Lowest Common Ancestor of a Binary Search Tree

{% embed url="https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/" %}

## Solution 1

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val   int
 *     Left  *TreeNode
 *     Right *TreeNode
 * }
 */

func lowestCommonAncestor(root, p, q *TreeNode) *TreeNode {
    if root == nil || p == nil || q == nil {
        return nil
    }
    if p.Val < root.Val && q.Val < root.Val {
        return lowestCommonAncestor(root.Left, p, q)
    }
    if p.Val > root.Val && q.Val > root.Val {
        return lowestCommonAncestor(root.Right, p, q)
    }
    return root
}
```
