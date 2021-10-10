---
description: ID: 127; medium
---
# Topological Sorting

{% embed url="https://www.lintcode.com/problem/127/" %}

## Solution 1 (Java)

```java
/**
 * Definition for Directed graph.
 * class DirectedGraphNode {
 *     int label;
 *     List<DirectedGraphNode> neighbors;
 *     DirectedGraphNode(int x) {
 *         label = x;
 *         neighbors = new ArrayList<DirectedGraphNode>();
 *     }
 * }
 */

public class Solution {
    /**
     * @param graph: A list of Directed graph node
     * @return: Any topological order for the given graph.
     */
    public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
        ArrayList<DirectedGraphNode> res = new ArrayList<>();
        Map<DirectedGraphNode, Integer> inDegree = new HashMap<>();
        for (DirectedGraphNode n : graph) {
            for (DirectedGraphNode nei : n.neighbors) {
                if (inDegree.containsKey(nei)) {
                    inDegree.put(nei, inDegree.get(nei) + 1);
                } else {
                    inDegree.put(nei, 1);
                }
            }
        }

        Queue<DirectedGraphNode> q = new ArrayDeque<>();
        for (DirectedGraphNode n : graph) {
            if (!inDegree.containsKey(n)) {
                q.offer(n);
            }
        }

        while (!q.isEmpty()) {
            DirectedGraphNode curr = q.poll();
            res.add(curr);
            for (DirectedGraphNode nei : curr.neighbors) {
                inDegree.put(nei, inDegree.get(nei) - 1);
                if (inDegree.get(nei) == 0) {
                    q.offer(nei);
                }
            }
        }

        return res;
    }
}
```

### Notes

* It is important to keep track of the in-degree of the nodes.
