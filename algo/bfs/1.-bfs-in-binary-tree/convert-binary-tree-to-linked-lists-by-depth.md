---
description: 'ID: 242; easy'
---

# Convert Binary Tree to Linked Lists by Depth

{% embed url="https://www.lintcode.com/problem/242/" %}

## Solution 1 \(Java\)

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    /**
     * @param root the root of binary tree
     * @return a lists of linked list
     */
    public List<ListNode> binaryTreeToLists(TreeNode root) {
        List<ListNode> res = new ArrayList<>();
        if (root == null) return res;
        Queue<TreeNode> q = new ArrayDeque<>();
        q.offer(root);

        while (!q.isEmpty()) {
            int n = q.size();
            ListNode dummy = new ListNode(0);
            ListNode head = dummy;
            for (int i = 0; i < n; i++) {
                TreeNode curr = q.poll();
                head.next = new ListNode(curr.val);
                head = head.next;
                if (curr.left != null)
                    q.offer(curr.left);
                if (curr.right != null)
                    q.offer(curr.right);
            }
            res.add(dummy.next);
        }

        return res;
    }
}
```

### Notes

* Note that we used a `dummy` node to construct the list.

