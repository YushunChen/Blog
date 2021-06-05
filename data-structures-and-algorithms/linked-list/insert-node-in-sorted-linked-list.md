---
description: 'ID: 219; easy; 在排序链表中插入一个节点'
---

# Insert Node in Sorted Linked List

{% embed url="https://www.lintcode.com/problem/219/" %}

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
     * @param head: The head of linked list.
     * @param val: An integer.
     * @return: The head of new linked list.
     */
    public ListNode insertNode(ListNode head, int val) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode cur = dummy;
        
        while (cur.next != null && cur.next.val <= val) {
            cur = cur.next;
        }

        ListNode newNode = new ListNode(val);
        newNode.next = cur.next;
        cur.next = newNode;

        return dummy.next;
    }
}
```

### Notes

* Find the first node in the list after which the new node should be inserted.

