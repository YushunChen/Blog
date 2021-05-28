# Binary Tree Postorder Traversal

{% embed url="https://leetcode.com/problems/binary-tree-postorder-traversal/" %}

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
func postorderTraversal(root *TreeNode) []int {
    res := make([]int, 0)
    postorderHelper(root, &res)
    return res
}

func postorderHelper(root *TreeNode, res *[]int) {
    if root != nil {
        postorderHelper(root.Left, res)
        postorderHelper(root.Right, res)
        *res = append(*res, root.Val)
    }
}
```

