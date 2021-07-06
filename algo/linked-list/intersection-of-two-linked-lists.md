---
description: 'ID: 160; easy'
---

# Intersection of Two Linked Lists

{% embed url="https://leetcode.com/problems/intersection-of-two-linked-lists/" %}

## Solution 1

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */

func getIntersectionNode(headA, headB *ListNode) *ListNode {
    lengthA, lengthB := getLength(headA), getLength(headB)
    ignore := lengthA - lengthB
    if ignore > 0 {
        for ignore > 0 {
            headA = headA.Next
            ignore--
        }
    } else if ignore < 0 {
        for ignore < 0 {
            headB = headB.Next
            ignore++
        }
    }
    for headA != nil && headB != nil {
        if headA == headB {
            return headA
        }
        if headA.Next == headB.Next {
            return headA.Next
        }
        headA = headA.Next
        headB = headB.Next
    }
    return nil
}

func getLength(root *ListNode) int {
    length := 0
    for root != nil {
        length++
        root = root.Next
    }
    return length
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

func getIntersectionNode(headA, headB *ListNode) *ListNode {
    if headA == nil || headB == nil {
        return nil
    }
    a, b := headA, headB
    // a little bit of trickery
    for a != b {
        if a == nil {
            a = headB
        } else {
            a = a.Next
        }
        if b == nil {
            b = headA
        } else {
            b = b.Next
        }
    }
    return a
}
```

