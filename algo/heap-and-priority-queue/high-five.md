---
description: 'ID: 613; medium'
---

# High Five

{% embed url="https://www.lintcode.com/problem/613/" %}

## Solution 1 \(Java\)

```java
/**
 * Definition for a Record
 * class Record {
 *     public int id, score;
 *     public Record(int id, int score){
 *         this.id = id;
 *         this.score = score;
 *     }
 * }
 */
public class Solution {
    /**
     * @param results a list of <student_id, score>
     * @return find the average of 5 highest scores for each person
     * Map<Integer, Double> (student_id, average_score)
     */
    public Map<Integer, Double> highFive(Record[] results) {
        Map<Integer, Double> ans = new HashMap<>();
        Map<Integer, PriorityQueue<Integer>> map = new HashMap<>();
        for (Record r : results) {
            map.putIfAbsent(r.id, new PriorityQueue<Integer>());
            PriorityQueue<Integer> pq = map.get(r.id);
            if (pq.size() < 5) {
                pq.offer(r.score);
            } else {
                if (r.score > pq.peek()) {
                    pq.poll();
                    pq.offer(r.score);
                }
            }
        }

        for (Map.Entry<Integer, PriorityQueue<Integer>> e : map.entrySet()) {
            int id = e.getKey();
            PriorityQueue<Integer> scores = e.getValue();
            double avg = 0;
            for (Integer s : scores) {
                avg += s;
            }
            avg /= 5.0;
            ans.put(id, avg);
        }

        return ans;
    }
}
```

