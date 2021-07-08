---
description: 'ID: 604; easy'
---

# Window Sum

{% embed url="https://www.lintcode.com/problem/604/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param nums: a list of integers.
     * @param k: length of window.
     * @return: the sum of the element inside the window at each moving.
     */
    public int[] winSum(int[] nums, int k) {
        if (nums == null || nums.length == 0 || nums.length < k) 
            return new int[0];
        int[] res = new int[nums.length - k + 1];
        int windowSum = 0;
        for (int i = 0; i < k; i++) {
            windowSum += nums[i];
        }
        for (int i = 0; i + k < nums.length; i++) {
            res[i] = windowSum;
            windowSum = windowSum - nums[i] + nums[i + k];
        }
        res[res.length - 1] = windowSum;
        return res;
    }
}
```

## Solution 2 \(Java\)

```java
public class Solution {
    /**
     * @param nums: a list of integers.
     * @param k: length of window.
     * @return: the sum of the element inside the window at each moving.
     */
    public int[] winSum(int[] nums, int k) {
        if (nums == null || nums.length == 0 || nums.length < k) 
            return new int[0];
        int[] res = new int[nums.length - k + 1];
        for (int i = 0; i < k; i++) {
            res[0] += nums[i];
        }
        for (int i = 1, j = k; j < nums.length; i++, j++) {
            res[i] = res[i - 1] - nums[i - 1] + nums[j];
        }
        return res;
    }
}
```

### Notes

* A better refactored version than [Solution 1](window-sum.md#solution-1-java). 
* Both solutions have the idea of **memoization** in mind.

