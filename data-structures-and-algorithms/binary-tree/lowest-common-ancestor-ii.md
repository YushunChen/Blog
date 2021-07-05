---
description: 'ID: 474; easy'
---

# Lowest Common Ancestor II

{% embed url="https://www.lintcode.com/problem/474/" %}

## Solution 1 \(Java\)

```java
/**
 * Definition of ParentTreeNode:
 * 
 * class ParentTreeNode {
 *     public ParentTreeNode parent, left, right;
 * }
 */


public class Solution {
    /*
     * @param root: The root of the tree
     * @param A: node in the tree
     * @param B: node in the tree
     * @return: The lowest common ancestor of A and B
     */
    public ParentTreeNode lowestCommonAncestorII(ParentTreeNode root, ParentTreeNode A, ParentTreeNode B) {
        List<ParentTreeNode> pathA = retrace(A);
        List<ParentTreeNode> pathB = retrace(B);
        int indexA = pathA.size() - 1;
        int indexB = pathB.size() - 1;

        ParentTreeNode lca = null;

        while(indexA >= 0 && indexB >= 0) {
            if (pathA.get(indexA) != pathB.get(indexB))
                break;
            lca = pathA.get(indexA);
            indexA--;
            indexB--;
        }

        return lca;
    }

    private List<ParentTreeNode> retrace(ParentTreeNode node) {
        List<ParentTreeNode> path = new ArrayList<>();
        while (node != null) {
            path.add(node);
            node = node.parent;
        }
        return path;
    }
}

// pathA: 3 4
// pathB: 5 7 4

// pathA: 5 7 4
// pathB: 6 7 4
```

### Notes

* This solution is straight-forward. We first find the path of the `A` and `B` nodes by retracing from their parent nodes.
* We compare these two paths from the last elements. The last element that the two paths share is the least common ancestor of `A` and `B`.

