---
description: 'ID: 650; medium; 二叉树叶子顺序遍历'
---

# Find Leaves of Binary Tree

{% embed url="https://www.lintcode.com/problem/650/" %}

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
     * @return: collect and remove all leaves
     */
    public List<List<Integer>> findLeaves(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        Map<Integer, List<Integer>> levels = new HashMap<>();

        int maxDepth = dfs(root, levels);
        for (int i = 1; i <= maxDepth; i++) {
            res.add(levels.get(i));
        }
        return res;
    }

    private int dfs(TreeNode root, Map<Integer, List<Integer>> levels) {
        if (root == null) return 0;
        int maxDepth = Math.max(dfs(root.left, levels), dfs(root.right, levels)) + 1;
        // 1 is the bottom level
        levels.putIfAbsent(maxDepth, new ArrayList<>());
        levels.get(maxDepth).add(root.val);
        return maxDepth;
    }
}
```

### Notes

* Use a `HashMap` to store the levels of the tree. The key is the level \(1 is the bottom level\) and the value of a list of node values.
* Use a similar mechanism in [Maximum Depth of Binary Tree](maximum-depth-of-binary-tree.md) and add a few operations to populate the map. 
* Lastly, convert the values in the map to a result list and return.

