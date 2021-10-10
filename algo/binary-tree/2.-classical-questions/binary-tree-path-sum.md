---
description: ID: 376; easy;  二叉树的路径和
---
# Binary Tree Path Sum

{% embed url="https://www.lintcode.com/problem/376/" %}

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
    /*
     * @param root: the root of binary tree
     * @param target: An integer
     * @return: all valid paths
     */
    public List<List<Integer>> binaryTreePathSum(TreeNode root, int target) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;
        List<Integer> path = new ArrayList<>();
        path.add(root.val);
        pathSumHelper(root, path, target, result);
        return result;
    }

    private void pathSumHelper(TreeNode root, List<Integer> path, int target, List<List<Integer>> result) {
        if (root.left == null && root.right == null) {
            if (root.val == target) {
                result.add(new ArrayList<Integer>(path));
            }
            return;
        }

        if (root.left != null) {
            path.add(root.left.val);
            pathSumHelper(root.left, path, target - root.val, result);
            path.remove(path.size() - 1);
        }

        if (root.right != null) {
            path.add(root.right.val);
            pathSumHelper(root.right, path, target - root.val, result);
            path.remove(path.size() - 1);
        }
    }
}
```
