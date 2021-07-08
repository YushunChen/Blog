---
description: 'ID: 98; medium'
---

# Sort List

{% embed url="https://www.lintcode.com/problem/98/" %}

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
     * @return: You should return the head of the sorted linked list, using constant space complexity.
     */
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null)
            return head;
        ListNode mid = findMid(head);
        ListNode right = sortList(mid.next);
        mid.next = null;
        ListNode left = sortList(head);
        return merge(left, right);
    }

    private ListNode findMid(ListNode head) {
        ListNode slow = head, fast = head.next;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

    private ListNode merge(ListNode left, ListNode right) {
        ListNode dummy = new ListNode(0);
        ListNode head = dummy;

        while (left != null && right != null) {
            if (left.val <= right.val) {
                head.next = left;
                left = left.next;
            } else {
                head.next = right;
                right = right.next;
            }
            head = head.next;
        }
        if (left != null) head.next = left;
        if (right != null) head.next = right;
        return dummy.next;
    }
}
```

### Notes

* This is the **merge sort** version of Sort List.
* Time complexity: `O(nlogn)`

## Solution 2 \(Java\)

```java

```

