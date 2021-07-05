---
description: 'ID: 628; easy'
---

# Maximum Subtree

{% embed url="https://www.lintcode.com/problem/628/" %}

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

    private int sum = Integer.MIN_VALUE;
    private TreeNode node = null;

    /**
     * @param root: the root of binary tree
     * @return: the maximum weight node
     */
    public TreeNode findSubtree(TreeNode root) {
        findSubtreeHelper(root);
        return node;
    }

    private int findSubtreeHelper(TreeNode root) {
        if (root == null)
            return 0;
        
        int left = findSubtreeHelper(root.left);
        int right = findSubtreeHelper(root.right);
        int currSum = root.val + left + right;
        if (currSum >= sum) {
            sum = currSum;
            node = root;
        }
        return currSum;
    }
}
```

### Notes

* Almost the same as [Minimum Subtree](minimum-subtree.md).

