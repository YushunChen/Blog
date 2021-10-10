---
description: ID: 597; easy
---
# Subtree with Maximum Average

{% embed url="https://www.lintcode.com/problem/597/" %}

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

    private class Result {
        int sum, num;
        public Result(int sum, int num) {
            this.sum = sum;
            this.num = num;
        }
    }

    private TreeNode maxAvgNode = null;
    private Result maxAvg = null;

    /**
     * @param root: the root of binary tree
     * @return: the root of the maximum average of subtree
     */
    public TreeNode findSubtree2(TreeNode root) {
        if (root == null)
            return null;
        dfs(root);
        return maxAvgNode;
    }

    private Result dfs(TreeNode root) {
        if (root == null)
            return new Result(0, 0);

        Result left = dfs(root.left);
        Result right = dfs(root.right);
        Result rootResult = new Result(left.sum + right.sum + root.val, left.num + right.num + 1);
        if (maxAvgNode == null || rootResult.sum * maxAvg.num > maxAvg.sum * rootResult.num) {
            maxAvg = rootResult;
            maxAvgNode = root;
        }
        return rootResult;
    }
}
```
