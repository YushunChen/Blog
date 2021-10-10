---
description: ID: 437; medium
---
# Path Sum III

{% embed url="https://leetcode.com/problems/path-sum-iii/" %}

## Solution 1 (Java)

```java
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
    public int pathSum(TreeNode root, int targetSum) {
        if (root == null)
                return 0;
        
        return pathSum(root.left, targetSum) 
            + pathSum(root.right, targetSum) + findPath(root, targetSum);
    }
    
    private int findPath(TreeNode root, int targetSum) {
        if (root == null)
            return 0;
        
        int res = 0;
        if (root.val == targetSum)
            res += 1;
        res += findPath(root.left, targetSum - root.val);
        res += findPath(root.right, targetSum - root.val);
        return res;
    }
}
```

### Notes

* `pathSum` returns the number of paths that have their sum equal to `targetSum` in the tree rooted at `root`. This include paths that starts at `root` and paths that do not start at `root`.
* `findPath` return the number of paths that have their sum equal to `targetSum`, but the paths must start at `root`.
