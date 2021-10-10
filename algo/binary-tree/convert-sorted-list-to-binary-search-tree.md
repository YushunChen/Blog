---
description: ID: 109; medium
---
# Convert Sorted List to Binary Search Tree

{% embed url="https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/" %}

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
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        if (head == null) return null;
        List<Integer> nums = new ArrayList<>();
        while (head != null) {
            nums.add(head.val);
            head = head.next;
        }
        return convert(nums, 0, nums.size() - 1);
    }
    
    private TreeNode convert(List<Integer> nums, int left, int right) {
        if (left > right) return null;
        int mid = left + (right - left) / 2;
        TreeNode root = new TreeNode(nums.get(mid));
        root.left = convert(nums, left, mid - 1);
        root.right = convert(nums, mid + 1, right);
        return root;
    }
}
```

### Notes

* We can convert the linked list to an array list. Then, we use the same method used in [Convert Sorted Array to Binary Search Tree](convert-sorted-array-to-binary-search-tree.md).
* Time complexity: `O(n)`
* Space complexity: `O(n)`

## Solution 2 (Java)

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
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        if (head == null) 
            return null;
        if (head.next == null) 
            return new TreeNode(head.val);
        ListNode slow = head, fast = head.next;
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        ListNode rootNode = slow.next;
        slow.next = null;
        
        TreeNode root = new TreeNode(rootNode.val);
        root.left = sortedListToBST(head);
        root.right = sortedListToBST(rootNode.next);
        return root;
    }
}
```

### Notes

* Using the same idea, we find the middle node of the linked list. It is important to note that we find the previous node of the middle node first (`slow` when the while loop ends). The reasons is that we need to cut the connection between the previous node and the middle node.
* Time complexity: `O(n)`
* Space complexity: `O(1)`
