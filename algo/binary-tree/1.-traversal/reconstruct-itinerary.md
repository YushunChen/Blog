---
description: 'ID: 1288; medium;'
---

# Reconstruct Itinerary

{% embed url="https://www.lintcode.com/problem/1288/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param tickets: 
     * @return: nothing
     */
    public List<String> findItinerary(List<List<String>> tickets) {
        Map<String, PriorityQueue<String>> map = new HashMap<>();
        for (List<String> ticket : tickets) {
            String from = ticket.get(0);
            String to = ticket.get(1);
            map.putIfAbsent(from, new PriorityQueue<String>());
            map.get(from).offer(to);
        }

        List<String> res = new ArrayList<>();
        Deque<String> stack = new ArrayDeque<>();
        stack.push("JFK");
        while (!stack.isEmpty()) {
            String from = stack.peek();
            PriorityQueue<String> tos = map.get(from);
            if (tos == null || tos.isEmpty()) {
                res.add(stack.pop());
                continue;
            }
            stack.push(tos.poll());
        }

        Collections.reverse(res);
        return res;
    }
}
```

### Notes

* Hierholzer's algorithm

