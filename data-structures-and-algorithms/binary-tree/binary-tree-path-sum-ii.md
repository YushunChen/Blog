---
description: 'ID: 246; medium; 二叉树的路径和 II'
---

# Binary Tree Path Sum II

{% embed url="https://www.lintcode.com/problem/246/" %}

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
    /*
     * @param root: the root of binary tree
     * @param target: An integer
     * @return: all valid paths
     */
    public List<List<Integer>> binaryTreePathSum2(TreeNode root, int target) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;
        List<Integer> path = new ArrayList<>();
        pathSumHelper(root, target, path, result);
        return result;
    }

    private void pathSumHelper(TreeNode root, int target, List<Integer> path, List<List<Integer>> result) {
        if (root == null) return;
        int sum = 0;
        path.add(root.val);
        for (int i = path.size() - 1; i >= 0; i--) {
            sum += path.get(i);
            if (sum == target) {
                result.add(new ArrayList<Integer>(path.subList(i, path.size())));
            }
        }
        pathSumHelper(root.left, target, path, result);
        pathSumHelper(root.right, target, path, result);
        path.remove(path.size() - 1);
    }
}
```

