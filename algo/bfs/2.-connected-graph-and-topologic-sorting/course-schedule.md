---
description: ID: 615; medium
---
# Course Schedule

{% embed url="https://www.lintcode.com/problem/615/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param numCourses: a total of n courses
     * @param prerequisites: a list of prerequisite pairs
     * @return: true if can finish all courses or false
     */
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        int[] degree = new int[numCourses];
        Map<Integer, List<Integer>> edges = new HashMap<>();
        for (int[] pre : prerequisites) {
            degree[pre[0]]++;
            if (!edges.containsKey(pre[1])) {
                edges.put(pre[1], new ArrayList<Integer>());
            }
            edges.get(pre[1]).add(pre[0]);
        }

        int num = 0;
        Queue<Integer> q = new ArrayDeque<>();
        for (int i = 0; i < degree.length; i++) {
            if (degree[i] == 0)
                q.offer(i);
        }
        
        while (!q.isEmpty()) {
            int curr = q.poll();
            num++;
            if (edges.containsKey(curr)) {
                for (int pre : edges.get(curr)) {
                    degree[pre]--;
                    if (degree[pre] == 0)
                        q.offer(pre);
                }
            }
        }

        return num == numCourses;
    }
}
```
