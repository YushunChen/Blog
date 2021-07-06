---
description: 'ID: 104; easy'
---

# Maximum Depth of Binary Tree

{% embed url="https://leetcode.com/problems/maximum-depth-of-binary-tree/" %}

{% embed url="https://www.lintcode.com/problem/97/" %}

## Solution 1 \(Golang\)

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func maxDepth(root *TreeNode) int {
    if root == nil {
        return 0
    }
    return max(maxDepth(root.Left), maxDepth(root.Right)) + 1
}

func max(x, y int) int {
    if x > y {
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
     * @param root: The root of binary tree.
     * @return: An integer
     */
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```

### Notes

*  Recursion with divide and conquer

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

    int maxDepth = 0;
    /**
     * @param root: The root of binary tree.
     * @return: An integer
     */
    public int maxDepth(TreeNode root) {
        maxDepthHelper(root, 1);
        return maxDepth;
    }

    private void maxDepthHelper(TreeNode root, int depth) {
        if (root == null) return;
        if (depth > maxDepth) maxDepth = depth;
        
        maxDepthHelper(root.left, depth + 1);
        maxDepthHelper(root.right, depth + 1);
    }
}
```

### Notes

*  Recursion with traversal

