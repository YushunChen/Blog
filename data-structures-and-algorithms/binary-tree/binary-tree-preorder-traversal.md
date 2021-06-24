# Binary Tree Preorder Traversal

{% embed url="https://leetcode.com/problems/binary-tree-preorder-traversal/" %}

{% embed url="https://www.lintcode.com/problem/66/" %}

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
func preorderTraversal(root *TreeNode) []int {
    res := make([]int, 0)
    preorderHelper(root, &res)
    return res
}

func preorderHelper(root *TreeNode, res *[]int) {
    if root != nil {
        *res = append(*res, root.Val)
        preorderHelper(root.Left, res)
        preorderHelper(root.Right, res)
    }
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
     * @param root: A Tree
     * @return: Preorder in ArrayList which contains node values.
     */
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        preorderTraversalHelper(root, result);
        return result;
    }

    private void preorderTraversalHelper(TreeNode root, List<Integer> result) {
        if (root == null) return;
        result.add(root.val);
        preorderTraversalHelper(root.left, result);
        preorderTraversalHelper(root.right, result);
    }
}
```

