---
description: ID: 472; hard; 二叉树的路径和 III
---
# Binary Tree Path Sum III

{% embed url="https://www.lintcode.com/problem/472/" %}

## Solution 1 (Java)

```java
/**
 * Definition of ParentTreeNode:
 * 
 * class ParentTreeNode {
 *     public int val;
 *     public ParentTreeNode parent, left, right;
 * }
 */


public class Solution {
    /*
     * @param root: the root of binary tree
     * @param target: An integer
     * @return: all valid paths
     */
    public List<List<Integer>> binaryTreePathSum3(ParentTreeNode root, int target) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;
        List<ParentTreeNode> allNodes = new ArrayList<>();
        inOrderTraversal(root, allNodes);
        for (ParentTreeNode node : allNodes) {
            HashSet<ParentTreeNode> set = new HashSet<>();
            List<Integer> path = new ArrayList<>();
            dfs(node, target, set, path, result);
        }
        return result;
    }

    private void inOrderTraversal(ParentTreeNode root, List<ParentTreeNode> allNodes) {
        if (root == null) return;
        inOrderTraversal(root.left, allNodes);
        allNodes.add(root);
        inOrderTraversal(root.right, allNodes);
    }

    private void dfs(ParentTreeNode root, int target, HashSet<ParentTreeNode> set, List<Integer> path, List<List<Integer>> result) {
        // HashSet to prevent infinite looping
        if (root == null || set.contains(root)) return;
        set.add(root);
        path.add(root.val);
        target -= root.val;
        if (target == 0) {
            List<Integer> pathCopy = new ArrayList<>(path);
            result.add(pathCopy);
        }

        // continue dfs on all directions
        dfs(root.left, target, set, path, result);
        dfs(root.right, target, set, path, result);
        dfs(root.parent, target, set, path, result);

        // reset the variables after done with one node
        set.remove(root);
        path.remove(path.size() - 1);
        target += root.val;
    }
}
```
