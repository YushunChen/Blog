---
description: 'ID: 61; medium'
---

# Rotate List

{% embed url="https://leetcode.com/problems/rotate-list/" %}

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
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || head.next == null) return head;
        ListNode dummy = new ListNode(0, head);
        k = k % findLengthOfList(head);
        while (k > 0) {
            ListNode secondToLastNode = findSecondToLastNode(dummy.next);
            ListNode lastNode = secondToLastNode.next;
            lastNode.next = dummy.next;
            dummy.next = lastNode;
            secondToLastNode.next = null;
            k--;
        }
        return dummy.next;        
    }
    
    public ListNode findSecondToLastNode(ListNode head) {
        while (head.next.next != null) {
            head = head.next;
        }
        return head;
    }
    
    public int findLengthOfList(ListNode head) {
        int length = 0;
        while (head != null) {
            head = head.next;
            length++;
        }
        return length;
    }
}
```

## Solution 2 \(Java\)

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
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || head.next == null || k == 0) {
            return head;
        }
        
        ListNode runner = head;
        int length = 1;
        while (runner.next != null) {
            runner = runner.next;
            length++;
        }
        
        // runner is the last node now
        runner.next = head;
        // a cycle is formed
        k %= length;
        k = length - k;
        while (k > 0) {
            runner = runner.next;
            k--;
        }
        // find the last node of the new list using k
        head = runner.next;
        runner.next = null;
        return head;
    }
}
```

