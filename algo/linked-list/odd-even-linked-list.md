---
description: ID: 328; medium
---
# Odd Even Linked List

{% embed url="https://leetcode.com/problems/odd-even-linked-list/" %}

## Solution 1

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func oddEvenList(head *ListNode) *ListNode {
    oddHead, evenHead := &ListNode{Val: 0}, &ListNode{Val: 0}
    oddRunner, evenRunner, index := oddHead, evenHead, 1
    for head != nil {
        if index % 2 != 0 {
            oddRunner.Next = head
            oddRunner = oddRunner.Next
        } else {
            evenRunner.Next = head
            evenRunner = evenRunner.Next
        }
        index++
        head = head.Next
    }
    oddRunner.Next = evenHead.Next
    evenRunner.Next = nil
    return oddHead.Next
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
func oddEvenList(head *ListNode) *ListNode {
    if head == nil {
        return nil
    }
    odd, even := head, head.Next
    evenHead := even
    for even != nil && even.Next != nil {
        odd.Next = even.Next
        odd = odd.Next
        even.Next = odd.Next
        even = even.Next
    }
    odd.Next = evenHead
    return head
}
```
