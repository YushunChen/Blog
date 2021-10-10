---
description: ID: 24; medium
---
# Swap Nodes in Pairs

{% embed url="https://leetcode.com/problems/swap-nodes-in-pairs/" %}

## Solution 1 (Java)

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
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode first = head;
        ListNode second = head.next;
        ListNode newHead = swapPairs(second.next);
        
        first.next = newHead;
        second.next = first;
        return second;
    }
}
```
