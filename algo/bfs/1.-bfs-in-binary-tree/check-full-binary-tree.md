---
description: 'ID: 726; medium'
---

# Check Full Binary Tree

{% embed url="https://www.lintcode.com/problem/726/" %}

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
 */

public class Solution {
    /**
     * @param root: the given tree
     * @return: Whether it is a full tree
     */
    public boolean isFullTree(TreeNode root) {
        if (root == null) return true;
        Queue<TreeNode> q = new ArrayDeque<>();
        q.offer(root);

        while (!q.isEmpty()) {
            TreeNode curr = q.poll();
            if (curr.left != null && curr.right == null) {
                return false;
            }
            if (curr.left == null && curr.right != null) {
                return false;
            }
            if (curr.left != null) {
                q.offer(curr.left);
            }
            if (curr.right != null) {
                q.offer(curr.right);
            }
        }
        return true;
    }
}
```

