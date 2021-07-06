---
description: 'ID: 450; hard; K组翻转链表'
---

# Reverse Nodes in k-Group

{% embed url="https://www.lintcode.com/problem/450/" %}

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
     * @param head: a ListNode
     * @param k: An integer
     * @return: a ListNode
     */
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode cur = dummy;

        while (true) {
            cur = reverseBetween(cur, k);
            if (cur == null) break;
        }
        return dummy.next;
    }


    // modified from Reverse Linked List II
    public ListNode reverseBetween(ListNode head, int k) {
        if (head == null) return head;

        // 1. find the k-th node 
        ListNode kNode = head;
        for (int i = 0; i < k; i++) {
            kNode = kNode.next;
            if (kNode == null) return null;
        }

        ListNode firstNode = head.next;
        ListNode kNextNode = kNode.next;

        // 2. reverse
        ListNode prev = null, next;
        ListNode curr = firstNode;
        while (curr != kNextNode) {
            next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }

        // 3. connect the lists
        head.next = kNode;
        firstNode.next = kNextNode;
        return firstNode;
    }
}
```

### Notes

* We use a similar approach used in [Reverse Linked List II](reverse-linked-list-ii.md). Using the helper function `reverseBetween`, we reverse `k` nodes each time and return the end of of the linked list for each `k` group. If the end node is null, we know that the remaining nodes cannot constitute a `k` group.
* Inside the helper function, note that the `head` is always one node before the starting node that is to be reversed. Then, we keep track of the first node that is to be reversed \(`firstNode`\) and the node after k-th node \(`kNextNode`\) because we need to connect the reversed linked list eventually with a start and an end.

