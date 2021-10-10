---
description: ID: 786; easy;
---
# Linked List Weighted Sum In Reverse Order

{% embed url="https://www.lintcode.com/problem/linked-list-weighted-sum-in-reverse-order/" %}

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

    int sum = 0;

    /**
     * @param head: the given linked list
     * @return: the array that store the values in reverse order 
     */
    public int weightedSumReverse(ListNode head) {
        reverseHelper(head);
        return sum;
    }

    private int reverseHelper(ListNode head) {
        if (head == null) return 0;
        int weight = reverseHelper(head.next);
        weight++;
        sum += weight * head.val;
        return weight;
    }
}
```

### Notes

* This is similar to [Reverse Order Storage](reverse-order-storage.md). The difference is that we increment the weight and return it to its upper level each time.
