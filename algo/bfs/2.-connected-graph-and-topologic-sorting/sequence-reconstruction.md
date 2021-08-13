---
description: 'ID: 605; medium'
---

# Sequence Reconstruction

{% embed url="https://www.lintcode.com/problem/605/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param org: a permutation of the integers from 1 to n
     * @param seqs: a list of sequences
     * @return: true if it can be reconstructed only one or false
     */
    public boolean sequenceReconstruction(int[] org, int[][] seqs) {
        Map<Integer, Set<Integer>> graph = buildGraph(seqs);
        List<Integer> topoOrder = getTopoOrder(graph);
        if (topoOrder == null || topoOrder.size() != org.length)
            return false;
        for (int i = 0; i < topoOrder.size(); i++) {
            if (topoOrder.get(i) != org[i])
                return false;
        }
        return true;
    }

    private Map<Integer, Set<Integer>> buildGraph(int[][] seqs) {
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        for (int[] seq : seqs) {
            for (int i = 0; i < seq.length; i++) {
                graph.putIfAbsent(seq[i], new HashSet<>());
            }
        }
        for (int[] seq : seqs) {
            for (int i = 1; i < seq.length; i++) {
                graph.get(seq[i - 1]).add(seq[i]);
            }
        }
        return graph;
    }

    private List<Integer> getTopoOrder(Map<Integer, Set<Integer>> graph) {
        Map<Integer, Integer> inDegree = getInDegree(graph);
        Queue<Integer> q = new ArrayDeque<>();
        List<Integer> topoOrder = new ArrayList<>();
        for (Integer n : inDegree.keySet()) {
            if (inDegree.get(n) == 0) {
                q.offer(n);
                topoOrder.add(n);
            }
        }

        while (!q.isEmpty()) {
            if (q.size() > 1) return null;
            Integer curr = q.poll();
            for (Integer neighbor : graph.get(curr)) {
                inDegree.put(neighbor, inDegree.get(neighbor) - 1);
                if (inDegree.get(neighbor) == 0) {
                    q.offer(neighbor);
                    topoOrder.add(neighbor);
                }
            }
        }
        return topoOrder.size() == graph.size() ? topoOrder : null;
    }

    private Map<Integer, Integer> getInDegree(Map<Integer, Set<Integer>> graph) {
        Map<Integer, Integer> inDegree = new HashMap<>();
        for (Integer n : graph.keySet()) {
            inDegree.put(n, 0);
        }
        for (Integer n : graph.keySet()) {
            for (Integer nei : graph.get(n)) {
                inDegree.put(nei, inDegree.get(nei) + 1);
            }
        }
        return inDegree;
    }
}
```

