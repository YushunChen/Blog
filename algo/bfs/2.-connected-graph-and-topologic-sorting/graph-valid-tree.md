---
description: ID: 178; medium
---
# Graph Valid Tree

{% embed url="https://www.lintcode.com/problem/178/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param n: An integer
     * @param edges: a list of undirected edges
     * @return: true if it's a valid tree, or false
     */
    public boolean validTree(int n, int[][] edges) {
        // condition check
        if (n == 0) return false;
        if (n - edges.length != 1) return false;

        // 1. construct graph
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        for (int i = 0; i < n; i++) {
            graph.put(i, new HashSet<Integer>());
        }
        for (int[] e : edges) {
            graph.get(e[0]).add(e[1]);
            graph.get(e[1]).add(e[0]);
        }

        // 2. BFS
        Queue<Integer> q = new ArrayDeque<>();
        Set<Integer> visited = new HashSet<>();
        q.offer(0);
        visited.add(0);

        while (!q.isEmpty()) {
            int curr = q.poll();
            for (int neighbor : graph.get(curr)) {
                if (!visited.contains(neighbor)) {
                    q.offer(neighbor);
                    visited.add(neighbor);
                }
            }
        }

        // condition check
        return visited.size() == n;
    }
}
```

### Notes

* In order to be a valid tree, the graph needs to satisfy the following three conditions:
  * The number of nodes - the number of edges = 1
  * No cycle
  * Only one connected graph
