---
description: 'ID: 160; easy'
---

# Intersection of Two Linked Lists

{% embed url="https://leetcode.com/problems/intersection-of-two-linked-lists/" %}

## Solution 1 (Go)

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

## Solution 2 (Go)

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

## Solution 3 (Java)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode currA = headA;
        ListNode currB = headB;
        
        while (currA != currB) {
            if (currA == null) {
                currA = headB;
            } else {
                currA = currA.next;
            }
            if (currB == null) {
                currB = headA;
            } else {
                currB = currB.next;
            }
        }
        return currA;
    }
}
```
