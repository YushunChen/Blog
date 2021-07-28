---
description: 'ID: 86; medium'
---

# Partition List

{% embed url="https://leetcode.com/problems/partition-list/" %}

## Solution 1 \(Java\)

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
    public ListNode partition(ListNode head, int x) {
        ListNode dummySmall = new ListNode(0);
        ListNode dummyLarge = new ListNode(0);
        ListNode headSmall = dummySmall;
        ListNode headLarge = dummyLarge;
        while (head != null) {
            if (head.val < x) {
                headSmall.next = head;
                headSmall = head;
            } else {
                headLarge.next = head;
                headLarge = head;
            }
            head = head.next;
        }
        headSmall.next = dummyLarge.next;
        headLarge.next = null;
        return dummySmall.next;
    }
}
```

