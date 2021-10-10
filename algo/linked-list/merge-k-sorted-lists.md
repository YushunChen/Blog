---
description: ID: 104; medium; 合并k个排序链表算法
---
# Merge K Sorted Lists

{% embed url="https://www.lintcode.com/problem/104/" %}

## Solution 1 (Java)

```java
/**
 * Definition for ListNode.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int val) {
 *         this.val = val;
 *         this.next = null;
 *     }
 * }
 */ 
public class Solution {
    /**
     * @param lists: a list of ListNode
     * @return: The head of one sorted list.
     */
    public ListNode mergeKLists(List<ListNode> lists) {  
        if (lists == null || lists.size() == 0)
            return null;
        return mergeHelper(lists, 0, lists.size() - 1);
    }

    private ListNode mergeHelper(List<ListNode> lists, int start, int end) {
        if (start == end) return lists.get(start);
        
        int mid = start + (end - start) / 2;
        ListNode leftHalf = mergeHelper(lists, start, mid);
        ListNode rightHalf = mergeHelper(lists, mid + 1, end);
        return mergeTwoLists(leftHalf, rightHalf);
    }
    
    // from Merge Two Sorted Lists
    private ListNode mergeTwoLists(ListNode l1, ListNode l2) {
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

### Notes

* This solution uses **divide and conquer**.
* Let `k` be the number of lists and `n` be the number of nodes in a list on average, then the time complexity is `O(nk * log(k))`. Also, the recursion uses the stack space, which is `O(n)`.

## Solution 2 (Java)

```java
/**
 * Definition for ListNode.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int val) {
 *         this.val = val;
 *         this.next = null;
 *     }
 * }
 */ 
public class Solution {
    /**
     * @param lists: a list of ListNode
     * @return: The head of one sorted list.
     */
    public ListNode mergeKLists(List<ListNode> lists) {  
        if (lists == null || lists.size() == 0)
            return null;
        
        Queue<ListNode> heap = new PriorityQueue<ListNode>(lists.size(), ListNodeComparator);
        for (int i = 0; i < lists.size(); i++) {
            if (lists.get(i) != null)
                heap.add(lists.get(i));
        }

        ListNode dummy = new ListNode(0);
        ListNode cur = dummy;
        while (!heap.isEmpty()) {
            ListNode head = heap.poll();
            cur.next = head;
            cur = cur.next;
            if (head.next != null)
                heap.add(head.next);
        }
        return dummy.next;
    }

    private Comparator<ListNode> ListNodeComparator = new Comparator<ListNode>() {
        public int compare(ListNode left, ListNode right) {
            return left.val - right.val;
        }
    };
}

```

### Notes

* This solution uses a **minimum heap** with the size of the lists. Each time, we grab a node from each list and add the smallest one to the linked list by the property of the min heap.

## Solution 3 (Java)

```java
/**
 * Definition for ListNode.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int val) {
 *         this.val = val;
 *         this.next = null;
 *     }
 * }
 */ 
public class Solution {
    /**
     * @param lists: a list of ListNode
     * @return: The head of one sorted list.
     */
    public ListNode mergeKLists(List<ListNode> lists) {  
        if (lists == null || lists.size() == 0)
            return null;
        
        while (lists.size() > 1) {
            List<ListNode> newLists = new ArrayList<ListNode>();
            for (int i = 0; i + 1 < lists.size(); i+=2) {
                ListNode twoMergedLists = mergeTwoLists(lists.get(i), lists.get(i+1));
                newLists.add(twoMergedLists);
            }
            if (lists.size() % 2 == 1) {
                newLists.add(lists.get(lists.size() - 1));
            }
            lists = newLists;
        }

        return lists.get(0);
    }

    // from Merge Two Sorted Lists
    private ListNode mergeTwoLists(ListNode l1, ListNode l2) {
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

### Notes

* This solution is straightforward. We simply merge the lists two by two, which is similar to a playoffs elimination table.
* Be careful if the number of lists is odd.
