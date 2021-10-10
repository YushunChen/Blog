---
description: ID: 1010; medium
---
# Pairs of Songs With Total Durations Divisible by 60

{% embed url="https://leetcode.com/problems/pairs-of-songs-with-total-durations-divisible-by-60/" %}

## Solution 1 (Java)

```java
class Solution {
    public int numPairsDivisibleBy60(int[] time) {
        Map<Integer, Integer> map = new HashMap<>();
        int res = 0;
        for (int i = 0; i < time.length; i++) {
            int t = time[i] % 60;
            if (t == 0 && map.containsKey(t)) {
                res += map.get(t);
            } else if (map.containsKey(60 - t)) {
                res += map.get(60 - t);
            }
            map.put(t, map.getOrDefault(t, 0) + 1);
        }
        return res;
    }
}
```
