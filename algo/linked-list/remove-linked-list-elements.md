---
description: ID: 203; easy
---
# Remove Linked List Elements

{% embed url="https://leetcode.com/problems/remove-linked-list-elements/" %}

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
    public ListNode removeElements(ListNode head, int val) {
        if (head == null) return null;
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode cur = head;
        
        ListNode prev = dummy;
        while (cur != null) {
            if (cur.val == val) {
                prev.next = cur.next;
            } else {
                prev = cur;
            }
            cur = cur.next;
        }
        return dummy.next;
    }
}
```

### Notes

* Be careful that we only update `prev` if we do not find a node with matching value and skip that node.
