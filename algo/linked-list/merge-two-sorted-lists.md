---
description: ID: 165; easy; 合并两个排序链表
---
# Merge Two Sorted Lists

{% embed url="https://www.lintcode.com/problem/165/" %}

{% embed url="https://leetcode.com/problems/merge-two-sorted-lists/" %}

## Solution 1 (Java)

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
     * @param l1: ListNode l1 is the head of the linked list
     * @param l2: ListNode l2 is the head of the linked list
     * @return: ListNode head of linked list
     */
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode cur = dummy;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                cur.next = l1;
                l1 = l1.next;
            } else {
                cur.next = l2;
                l2 = l2.next;
            }
            cur = cur.next;
        }

        if (l1 == null) cur.next = l2;
        if (l2 == null) cur.next = l1;

        return dummy.next;
    }
}
```
