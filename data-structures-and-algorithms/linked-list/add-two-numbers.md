---
description: 'ID: 2; medium'
---

# Add Two Numbers

{% embed url="https://leetcode.com/problems/add-two-numbers/" %}

## Solution 1

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
    head := &ListNode{Val: 0}   // dummy node
    val1, val2, carry, runner := 0, 0, 0, head
    for l1 != nil || l2 != nil || carry == 1 {
        if l1 == nil {
            val1 = 0
        } else {
            val1 = l1.Val
            l1 = l1.Next
        }
        if l2 == nil {
            val2 = 0
        } else {
            val2 = l2.Val
            l2 = l2.Next
        }
        runner.Next = &ListNode{Val: (val1 + val2 + carry) % 10}
        carry = (val1 + val2 + carry) / 10
        runner = runner.Next
    }
    return head.Next
}
```

