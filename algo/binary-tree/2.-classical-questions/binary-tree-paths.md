---
description: ID: 257; easy
---
# Binary Tree Paths

{% embed url="https://leetcode.com/problems/binary-tree-paths/" %}

{% embed url="https://www.lintcode.com/problem/480/" %}

## Solution 1 (Go)

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */

import "strconv"

func binaryTreePaths(root *TreeNode) []string {
    if root == nil {
        return []string{}
    }
    if root.Left == nil && root.Right == nil {
        return []string{strconv.Itoa(root.Val)}
    }
    result := make([]string, 0)
    leftPaths := binaryTreePaths(root.Left)
    for _,lp := range leftPaths {
        result = append(result, strconv.Itoa(root.Val) + "->" + lp)
    }
    rightPaths := binaryTreePaths(root.Right)
    for _,rp := range rightPaths {
        result = append(result, strconv.Itoa(root.Val) + "->" + rp)
    }
    return result
}
```

## Solution 2 (Java)

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
     * @param root: the root of the binary tree
     * @return: all root-to-leaf paths
     */
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> result = new ArrayList<>();
        if (root == null) return result;
        dfs(root, String.valueOf(root.val), result);
        return result;
    }

    private void dfs(TreeNode root, String path, List<String> result) {
        if (root == null) return;
        if (root.left == null && root.right == null)
            result.add(path);
        if (root.left != null)
            dfs(root.left, path + "->" + root.left.val, result);
        if (root.right != null)
            dfs(root.right, path + "->" + root.right.val, result);
    }
}
```

### Notes

* This solution computes paths as strings, which is shorter and perhaps more straightforward to understand.

## Solution 3 (Java)

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
     * @param root: the root of the binary tree
     * @return: all root-to-leaf paths
     */
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> result = new ArrayList<>();
        List<TreeNode> path = new ArrayList<>();
        path.add(root);
        dfs(root, path, result);
        return result;
    }

    private void dfs(TreeNode root, List<TreeNode> path, List<String> result) {
        if (root == null) return;
        if (root.left == null && root.right == null) {
            String str = "";
            for (int i = 0; i < path.size(); i++) {
                if (i > 0) str += "->";
                str += path.get(i).val;
            }
            result.add(str);
            return;
        }
        path.add(root.left);
        dfs(root.left, path, result);
        path.remove(path.size() - 1);

        path.add(root.right);
        dfs(root.right, path, result);
        path.remove(path.size() - 1);
    }
}
```

### Notes

* This solution computes paths as paths, which is a similar approach used in [Binary Tree Path Sum](binary-tree-path-sum.md).
