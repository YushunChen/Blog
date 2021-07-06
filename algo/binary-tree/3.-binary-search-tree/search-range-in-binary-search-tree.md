---
description: 'ID: 11; medium; 二叉查找树中搜索区间'
---

# Search Range in Binary Search Tree

{% embed url="https://www.lintcode.com/problem/11/" %}

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

    private List<Integer> res;
    
    /**
     * @param root: param root: The root of the binary search tree
     * @param k1: An integer
     * @param k2: An integer
     * @return: return: Return all keys that k1<=key<=k2 in ascending order
     */
    public List<Integer> searchRange(TreeNode root, int k1, int k2) {
        res = new ArrayList<Integer>();
        searchRangeHelper(root, k1, k2);
        return res;
    }

    private void searchRangeHelper(TreeNode root, int k1, int k2) {
        if (root == null)
            return;

        // similar to inorder traversal to ensure ascending order
        if (root.val > k1)
            searchRangeHelper(root.left, k1, k2);
        if (root.val >= k1 && root.val <= k2)
            res.add(root.val);
        if (root.val < k2)
            searchRangeHelper(root.right, k1, k2);
    }
}
```

