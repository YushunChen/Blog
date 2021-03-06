---
description: ID: 481; easy; 二叉树叶子节点之和
---
# Binary Tree Leaf Sum

{% embed url="https://www.lintcode.com/problem/481/" %}

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
    /**
     * @param root: the root of the binary tree
     * @return: An integer
     */
    public int leafSum(TreeNode root) {
        if (root == null) 
            return 0;

        if (root.left == null && root.right == null)
            return root.val;
            
        return leafSum(root.left) + leafSum(root.right);    
    }
}
```

### Notes

* Divide and conquer

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

    private int sum;

    /**
     * @param root: the root of the binary tree
     * @return: An integer
     */
    public int leafSum(TreeNode root) {
        sum = 0;
        leafSumHelper(root);
        return sum;
    }

    private void leafSumHelper(TreeNode root) {
        if (root == null) return;
        if (root.left == null && root.right == null) {
            sum += root.val;
            return;
        }
        leafSumHelper(root.left);
        leafSumHelper(root.right);
    }
}
```

### Notes

* Traversal
