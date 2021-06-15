---
description: 'ID: 822; easy; 相反的顺序存储'
---

# Reverse Order Storage

{% embed url="https://www.lintcode.com/problem/822/" %}

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
     * @param head: the given linked list
     * @return: the array that store the values in reverse order 
     */
    public List<Integer> reverseStore(ListNode head) {
        List<Integer> arr = new ArrayList<Integer>();
        storeHelper(head, arr);
        return arr;
    }

    private void storeHelper(ListNode head, List<Integer> arr) {
        if (head == null) return;
        storeHelper(head.next, arr);
        arr.add(head.val);
    }
}
```

