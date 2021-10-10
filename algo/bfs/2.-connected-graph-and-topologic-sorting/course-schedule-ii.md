---
description: ID: 616; medium
---
# Course Schedule II

{% embed url="https://www.lintcode.com/problem/616/" %}

## Solution 1 (Java)

```java
public class Solution {
    /*
     * @param numCourses: a total of n courses
     * @param prerequisites: a list of prerequisite pairs
     * @return: the course order
     */
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        int[] degree = new int[numCourses];
        int[] order = new int[numCourses];
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
            order[num] = curr;
            num++;
            if (edges.containsKey(curr)) {
                for (int pre : edges.get(curr)) {
                    degree[pre]--;
                    if (degree[pre] == 0)
                        q.offer(pre);
                }
            }
        }

        return num == numCourses ? order : new int[0];
    }
}
```

### Notes

* Almost the same as [Course Schedule](course-schedule.md).
