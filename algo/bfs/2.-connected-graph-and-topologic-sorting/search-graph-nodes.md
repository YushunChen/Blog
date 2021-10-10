---
description: ID: 618; medium
---
# Search Graph Nodes

{% embed url="https://www.lintcode.com/problem/618/" %}

## Solution 1 (Java)

```java
/**
 * Definition for graph node.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { 
 *         label = x; neighbors = new ArrayList<UndirectedGraphNode>(); 
 *     }
 * };
 */


public class Solution {
    /*
     * @param graph: a list of Undirected graph node
     * @param values: a hash mapping, <UndirectedGraphNode, (int)value>
     * @param node: an Undirected graph node
     * @param target: An integer
     * @return: a node
     */
    public UndirectedGraphNode searchNode(ArrayList<UndirectedGraphNode> graph,
                                          Map<UndirectedGraphNode, Integer> values,
                                          UndirectedGraphNode node,
                                          int target) {
        if (graph == null || graph.size() == 0)
            return null;
        Queue<UndirectedGraphNode> q = new ArrayDeque<>();
        Set<UndirectedGraphNode> visited = new HashSet<>();
        q.offer(node);
        visited.add(node);

        while (!q.isEmpty()) {
            UndirectedGraphNode cur = q.poll();
            if (values.get(cur) == target) return cur;
            for (UndirectedGraphNode n : cur.neighbors) {
                if (!visited.contains(n)) {
                    q.offer(n);
                    visited.add(n);
                }
            }
        }
        return null;
    }
}
```
