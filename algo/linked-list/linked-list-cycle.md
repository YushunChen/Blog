---
description: ID: 141; easy
---
# Linked List Cycle

{% embed url="https://leetcode.com/problems/linked-list-cycle/" %}

{% embed url="https://www.lintcode.com/problem/102/" %}

## Solution 1 (Go)

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func hasCycle(head *ListNode) bool {
    m := make(map[*ListNode]bool)
    for head != nil {
        if _,found := m[head]; found {
            return true
        }
        m[head] = true
        head = head.Next
    }
    return false
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
func hasCycle(head *ListNode) bool {
    tortoise, hare := head, head
    for tortoise != nil && hare != nil && hare.Next != nil {
        tortoise = tortoise.Next
        hare = hare.Next.Next
        if tortoise == hare {
            return true
        }
    }
    return false
    
}
```

## Solution 3 (Java)

```java
/**
 * Definition for ListNode
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
    /**
     * @param head: The first node of linked list.
     * @return: True if it has a cycle, or false
     */
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null)
            return false;
        
        ListNode slow = head;
        ListNode fast = head;
        
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) return true;
        }

        return false;
    }
}
```

### Floyd's tortoise and hare cycle-finding algorithm

{% embed url="https://en.wikipedia.org/wiki/Cycle_detection#Floyd's_tortoise_and_hare" %}

The tortoise move by 1 step each time and the hare moves by 2 steps at a time. If there is a cycle, the hare will eventually catch the tortoise at a position.

A simple idea of the proof can be tracking the **gap** between the tortoise and the hare. By construction, the gap increases by 1 each iteration. Eventually, the gap with become n, where n is the number of elements in the **cycle** (not the whole list). This is the time when the tortoise and the hare meet. More proofs:

{% embed url="https://math.stackexchange.com/questions/913499/proof-of-floyd-cycle-chasing-tortoise-and-hare" %}
