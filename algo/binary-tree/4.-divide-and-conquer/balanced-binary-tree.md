---
description: ID: 110; easy
---
# Balanced Binary Tree

{% embed url="https://leetcode.com/problems/balanced-binary-tree/" %}

{% embed url="https://www.lintcode.com/problem/93/" %}

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

func isBalanced(root *TreeNode) bool {
    if root == nil {
        return true
    }
    leftDepth := depthHelper(root.Left)
    rightDepth := depthHelper(root.Right)
    if abs(leftDepth - rightDepth) > 1 {
        return false
    }
    return isBalanced(root.Left) && isBalanced(root.Right)
}

func depthHelper(root *TreeNode) int {
    if root == nil {
        return 0
    } 
    return max(depthHelper(root.Left), depthHelper(root.Right)) + 1
}

func max(x, y int) int {
    if x > y {
        return x
    }
    return y
}

func abs(x int) int {
    if x >= 0 {
        return x
    }
    return -x
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
     * @param root: The root of binary tree.
     * @return: True if this Binary tree is Balanced, or false.
     */
    public boolean isBalanced(TreeNode root) {
        if (root == null)
            return true;
        
        int leftDepth = depthHelper(root.left);
        int rightDepth = depthHelper(root.right);
        if (Math.abs(leftDepth - rightDepth) > 1)
            return false;

        return isBalanced(root.left) && isBalanced(root.right);
    }

    private int depthHelper(TreeNode root) {
        if (root == null)
            return 0;
        
        int left = depthHelper(root.left);
        int right = depthHelper(root.right);
        return Math.max(left, right) + 1;
    }
}
```

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

    private boolean balanced = true;
    /**
     * @param root: The root of binary tree.
     * @return: True if this Binary tree is Balanced, or false.
     */
    public boolean isBalanced(TreeNode root) {
        depthHelper(root);
        return balanced;
    }

    private int depthHelper(TreeNode root) {
        if (root == null)
            return 0;
        
        int left = depthHelper(root.left);
        int right = depthHelper(root.right);
        if (Math.abs(left - right) > 1)
            balanced = false;
            
        return Math.max(left, right) + 1;
    }
}
```

### Notes

* The refactored version of [Solution 2](balanced-binary-tree.md#solution-2-java).
* Solution 2 should be easier to follow and understand.
