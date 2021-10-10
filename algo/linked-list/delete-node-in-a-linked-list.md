---
description: ID: 237; easy
---
# Delete Node in a Linked List

{% embed url="https://leetcode.com/problems/delete-node-in-a-linked-list/" %}

## Solution 1

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func deleteNode(node *ListNode) {
    node.Val = node.Next.Val
    node.Next = node.Next.Next
}
```

## Solution 2

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func deleteNode(node *ListNode) {
    if node == nil {
        return
    }
    runner := node
    for runner.Next.Next != nil {
        runner.Val = runner.Next.Val
        runner = runner.Next
    }
    runner.Val = runner.Next.Val
    runner.Next = nil
}
```

