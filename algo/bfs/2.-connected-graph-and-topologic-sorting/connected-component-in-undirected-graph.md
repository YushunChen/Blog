---
description: 'ID: 431; medium'
---

# Connected Component in Undirected Graph

{% embed url="https://www.lintcode.com/problem/431/" %}

## Solution 1 \(Java\)

```java
/**
 * Definition for Undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     List<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) {
 *         label = x;
 *         neighbors = new ArrayList<UndirectedGraphNode>();
 *     }
 * }
 */

public class Solution {
    /**
     * @param nodes: a array of Undirected graph node
     * @return: a connected set of a Undirected graph
     */
    public List<List<Integer>> connectedSet(List<UndirectedGraphNode> nodes) {
        List<List<Integer>> res = new ArrayList<>();
        Set<UndirectedGraphNode> visited = new HashSet<>();
        for (UndirectedGraphNode node : nodes) {
            if (!visited.contains(node)) {
                bfs(node, res, visited);
            }
        }
        return res;
    }

    private void bfs(UndirectedGraphNode node, List<List<Integer>> res, Set<UndirectedGraphNode> visited) {
        Queue<UndirectedGraphNode> q = new ArrayDeque<>();
        List<Integer> component = new ArrayList<>();
        q.offer(node);
        visited.add(node);

        while (!q.isEmpty()) {
            UndirectedGraphNode curr = q.poll();
            component.add(curr.label);
            for (UndirectedGraphNode n : curr.neighbors) {
                if (!visited.contains(n)) {
                    q.offer(n);
                    visited.add(n);
                }
            }  
        }
        Collections.sort(component);
        res.add(component);
    }
}
```

