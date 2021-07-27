---
description: 'ID: 36; medium; 翻转链表（二）'
---

# Reverse Linked List II

{% embed url="https://www.lintcode.com/problem/36/" %}

{% embed url="https://leetcode.com/problems/reverse-linked-list-ii/" %}

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

### Notes

We have three major steps here:

1. We first proceed to the \(m-1\)-th node, which is the node before the m-th node. Then we keep track of both of them.
2. We reverse from m to n using the same technique used in the classical [reverse linked list](reverse-linked-list.md).
3. Lastly, do not forget to connect the middle part, i.e., the reversed linked list, with `mPrev` and `cur` pointer.

```java
m = 2, n = 4;

     mPrev      mNode             n
step1: 1------->2------->3------->4------->5------->6

     mPrev      mNode            prev     cur
step2: 1        2<-------3<-------4        5------->6

     mPrev    prev              mNode     cur
step3: 1------->4------->3------->2------->5------->6
```

