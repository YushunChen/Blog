---
description: 'ID: 36; medium; 翻转链表（二）'
---

# Reverse Linked List II

{% embed url="https://www.lintcode.com/problem/36/" %}

## Solution 1 \(Java\)

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
     * @param head: ListNode head is the head of the linked list 
     * @param m: An integer
     * @param n: An integer
     * @return: The head of the reversed ListNode
     */
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if (head == null || head.next == null)
            return head;
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode cur = dummy;

        // 1. proceed to m's previous node
        for (int i = 0; i < m - 1; i++) {
            if (cur == null) return null;
            cur = cur.next;
        }

        // 2. reverse from m to n
        ListNode mPrev = cur;
        ListNode mNode = cur.next;
        cur = cur.next;
        ListNode prev = null, next;
        for (int i = m; i <= n; i++) {
            if (cur == null) return null;
            next = cur.next;
            cur.next = prev;
            prev = cur;
            cur = next;
        }

        // 3. connect the lists
        mPrev.next = prev;
        mNode.next = cur;
        return dummy.next;
    }
}
```



