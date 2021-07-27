---
description: 'ID: 2; medium'
---

# Add Two Numbers

{% embed url="https://leetcode.com/problems/add-two-numbers/" %}

## Solution 1 \(Go\)

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

## Solution 2 \(Java\)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode head = dummy;
        int carry = 0;
        while (l1 != null && l2 != null) {
            int val = (l1.val + l2.val + carry) % 10;
            carry = (l1.val + l2.val + carry) / 10;
            ListNode newNode = new ListNode(val);
            head.next = newNode;
            head = newNode;
            l1 = l1.next;
            l2 = l2.next;
        }
        while (l1 == null && l2 != null)  {
            int val = (l2.val + carry) % 10;
            carry = (l2.val + carry) / 10;
            ListNode newNode = new ListNode(val);
            head.next = newNode;
            head = newNode;
            l2 = l2.next;
        }
        while (l2 == null && l1 != null)  {
            int val = (l1.val + carry) % 10;
            carry = (l1.val + carry) / 10;
            ListNode newNode = new ListNode(val);
            head.next = newNode;
            head = newNode;
            l1 = l1.next;
        }
        if (carry == 1) head.next = new ListNode(1);
        return dummy.next;
    }
}

//     9 -> 9 -> 9 -> 9
//     9 -> 9
//     8 -> 9 -> 0 -> 0 -> 1
```

