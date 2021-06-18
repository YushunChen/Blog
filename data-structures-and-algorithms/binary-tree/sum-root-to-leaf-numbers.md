---
description: 'ID: 1353; medium; 根节点到叶节点求和'
---

# Sum Root to Leaf Numbers

{% embed url="https://www.lintcode.com/problem/1353/" %}

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
    /**
     * @param root: the root of the tree
     * @return: the total sum of all root-to-leaf numbers
     */
    public int sumNumbers(TreeNode root) {
        if (root == null) return 0;
        return dfs(root, 0);
    }

    private int dfs(TreeNode root, int num) {
        if (root == null) return 0;
        num = num * 10 + root.val;
        if (root.left == null && root.right == null)
            return num;
        int leftNum = dfs(root.left, num);
        int rightNum = dfs(root.right, num);
        return leftNum + rightNum;
    }
}
```

### Notes

* Divide and conquer

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

    private int sum = 0;

    /**
     * @param root: the root of the tree
     * @return: the total sum of all root-to-leaf numbers
     */
    public int sumNumbers(TreeNode root) {
        if (root == null) return sum;
        dfs(root, root.val);
        return sum;
    }

    private void dfs(TreeNode root, int num) {
        if (root == null) return;
        if (root.left == null && root.right == null) {
            sum += num;
            return;
        }
        if (root.left != null)
            dfs(root.left, num * 10 + root.left.val);
        if (root.right != null)
            dfs(root.right, num * 10 + root.right.val);
    }
}
```

### Notes

* Traversal

