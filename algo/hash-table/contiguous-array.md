---
description: 'ID: 525; medium'
---

# Contiguous Array

{% embed url="https://leetcode.com/problems/contiguous-array/" %}

{% embed url="https://www.lintcode.com/problem/994/" %}

## Solution 1 \(Java\)

```java
class Solution {
    public int findMaxLength(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);
        int maxLen = 0, sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum = sum + (nums[i] == 1 ? 1 : -1);
            if (map.containsKey(sum)) {
                maxLen = Math.max(maxLen, i - map.get(sum));
            } else {
                map.put(sum, i);
            }
        }
        return maxLen;
    }
}
```

