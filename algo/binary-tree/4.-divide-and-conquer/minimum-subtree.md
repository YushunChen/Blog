---
description: ID: 596; easy; 最小子树
---
# Minimum Subtree

{% embed url="https://www.lintcode.com/problem/596/" %}

## Solution 1 (Java)

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

    private int sum = Integer.MAX_VALUE;
    private TreeNode node = null;

    /**
     * @param root: the root of binary tree
     * @return: the root of the minimum subtree
     */
    public TreeNode findSubtree(TreeNode root) {
        findSubtreeHelper(root);
        return node;
    }

    private int findSubtreeHelper(TreeNode root) {
        if (root == null)
            return 0;
        
        int currSum = root.val + findSubtreeHelper(root.left) + findSubtreeHelper(root.right);
        if (currSum <= sum) {
            sum = currSum;
            node = root;
        }
        return currSum;
    }
}
```
