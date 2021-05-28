# Binary Tree Preorder Traversal

{% embed url="https://leetcode.com/problems/binary-tree-preorder-traversal/" %}

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
func preorderTraversal(root *TreeNode) []int {
    res := make([]int, 0)
    preorderHelper(root, &res)
    return res
}

func preorderHelper(root *TreeNode, res *[]int) {
    if root != nil {
        *res = append(*res, root.Val)
        preorderHelper(root.Left, res)
        preorderHelper(root.Right, res)
    }
}
```

