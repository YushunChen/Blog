---
description: 'ID: 129; medium'
---

# Rehashing

{% embed url="https://www.lintcode.com/problem/129/" %}

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
     * @param hashTable: A list of The first node of linked list
     * @return: A list of The first node of linked list which have twice size
     */    
    public ListNode[] rehashing(ListNode[] hashTable) {
        int cap = hashTable.length * 2;
        ListNode[] newHashTable = new ListNode[cap];
        for (ListNode node : hashTable) {
            while (node != null) {
                int index = (node.val % cap + cap) % cap;
                ListNode newNode = new ListNode(node.val);
                if (newHashTable[index] == null) {
                    newHashTable[index] = newNode;
                } else {
                    ListNode head = newHashTable[index];
                    while (head.next != null) {
                        head = head.next;
                    }
                    head.next = newNode;
                }
                node = node.next;
            }
        }
        return newHashTable;
    }
};
```

