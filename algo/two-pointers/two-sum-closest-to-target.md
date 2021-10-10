---
description: ID: 533; medium
---
# Two Sum - Closest to target

{% embed url="https://www.lintcode.com/problem/533/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param nums: an integer array
     * @param target: An integer
     * @return: the difference between the sum and the target
     */
    public int twoSumClosest(int[] nums, int target) {
        int minDiff = Integer.MAX_VALUE;
        if (nums == null || nums.length < 2)
            return minDiff;
        Arrays.sort(nums);

        int left = 0, right = nums.length - 1;
        while (left < right) {
            int diff = target - nums[left] - nums[right];
            minDiff = Math.min(minDiff, Math.abs(diff));
            if (diff == 0) return 0;
            if (diff > 0) {
                left++;
            } else {
                right--;
            }
        }
        return minDiff;
    }
}
```

### Notes

* We sort the array first using the built-in method.
* Then, we update the minimum difference when possible and we use the opposite two pointers to keep track of the difference. 
* Make sure to add absolute value for `diff` as required by the problem.
