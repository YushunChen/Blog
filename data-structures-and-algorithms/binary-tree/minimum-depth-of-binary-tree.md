---
description: 'ID: 111; easy'
---

# Minimum Depth of Binary Tree

{% embed url="https://leetcode.com/problems/minimum-depth-of-binary-tree/" %}

{% embed url="https://www.lintcode.com/problem/155/" %}

## Solution 1 \(Go\)

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func minDepth(root *TreeNode) int {
    if root == nil {
        return 0
    }
    if root.Right == nil {
        return minDepth(root.Left) + 1
    }
    if root.Left == nil {
        return minDepth(root.Right) + 1
    }
    return min(minDepth(root.Left), minDepth(root.Right)) + 1
}

func min(x, y int) int {
    if x < y {
        return x
    }
    return y
}
```

## Solution 2 \(Java\)

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
     * @param root: The root of binary tree
     * @return: An integer
     */
    public int minDepth(TreeNode root) {
        if (root == null) 
            return 0;
        if (root.left == null)
            return minDepth(root.right) + 1;
        if (root.right == null)
            return minDepth(root.left) + 1;
        int leftDepth = minDepth(root.left);
        int rightDepth = minDepth(root.right);
        return Math.min(leftDepth, rightDepth) + 1;
    }
}
```

### Notes

* Divide and conquer

## Solution 3 \(Java\)

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
     * @param root: The root of binary tree
     * @return: An integer
     */
    public int minDepth(TreeNode root) {
        if (root == null) 
            return 0;
        return minDepthHelper(root);
    }

    private int minDepthHelper(TreeNode root) {
        if (root == null) 
            return Integer.MAX_VALUE;
        if (root.left == null && root.right == null)
            return 1;
        return Math.min(minDepthHelper(root.left), minDepthHelper(root.right)) + 1;

    }
}
```

### Notes

* Divide and conquer slight variant

## Solution 4 \(Java\)

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

    private int ans = Integer.MAX_VALUE;

    /**
     * @param root: The root of binary tree
     * @return: An integer
     */
    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        dfs(root, 1);
        return ans;
    }

    private void dfs(TreeNode root, int depth) {
        if (root == null) return;
        if (root.left == null && root.right == null) {
            ans = Math.min(ans, depth);
            return;
        }
        dfs(root.left, depth + 1);
        dfs(root.right, depth + 1);
    }


}
```

### Notes

* Traversal

