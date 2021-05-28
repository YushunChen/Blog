---
description: 'ID: 206; easy'
---

# Reverse Linked List

{% embed url="https://leetcode.com/problems/reverse-linked-list/" %}

## Solution 1

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseList(head *ListNode) *ListNode {
    var before *ListNode
    for head != nil {
        after := head.Next
        head.Next = before
        before = head
        head = after
    }
    return before
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
func reverseList(head *ListNode) *ListNode {
    if head == nil || head.Next == nil {
        return head
    }
    newHead := reverseList(head.Next)
    head.Next.Next = head
    head.Next = nil
    return newHead
}
```

