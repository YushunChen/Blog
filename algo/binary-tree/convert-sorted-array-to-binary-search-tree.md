---
description: ID; 108; easy
---
# Convert Sorted Array to Binary Search Tree

{% embed url="https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/" %}

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
func sortedArrayToBST(nums []int) *TreeNode {
    if len(nums) == 0 {
        return nil
    }
    n := TreeNode{
        Val: nums[len(nums)/2],
        Left: sortedArrayToBST(nums[:len(nums)/2]),
        Right: sortedArrayToBST(nums[len(nums)/2+1:]),
    }
    return &n
}
```
