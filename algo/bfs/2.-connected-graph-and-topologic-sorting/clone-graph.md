---
description: 'ID: 137; medium'
---

# Clone Graph

{% embed url="https://www.lintcode.com/problem/137/" %}

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
     * @param node: A undirected graph node
     * @return: A undirected graph node
     */
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if (node == null) return node;
        Map<UndirectedGraphNode, UndirectedGraphNode> oldToNew = new HashMap<>();
        Queue<UndirectedGraphNode> q = new ArrayDeque<>();
        q.offer(node);
        oldToNew.put(node, new UndirectedGraphNode(node.label));

        while (!q.isEmpty()) {
            UndirectedGraphNode curr = q.poll();
            for (UndirectedGraphNode nei : curr.neighbors) {
                if (!oldToNew.containsKey(nei)) {
                    oldToNew.put(nei, new UndirectedGraphNode(nei.label));
                    q.offer(nei);
                }
                oldToNew.get(curr).neighbors.add(oldToNew.get(nei));
            }
        }
        return oldToNew.get(node);
    }
}
```

### Notes

* The `oldToNew` map has two functions here:
  * It keeps track of which nodes are visited. If the map already contains a node, we do not add it to the queue.
  * It creates a mapping between old nodes and new nodes. We can directly get new node from their corresponding old nodes.

