---
description: ID: 617; medium; 子数组的最大平均值 II
---
# Maximum Average Subarray II

{% embed url="https://www.lintcode.com/problem/617/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param nums: an array with positive and negative numbers
     * @param k: an integer
     * @return: the maximum average
     */
    public double maxAverage(int[] nums, int k) {
        if (nums == null || nums.length == 0 || k > nums.length) 
            return -1;

        double left, right, mid;
        left = right = nums[0];
        double delta = 1e-6;

        for (int n : nums) {
            left = Math.min(n, left);
            right = Math.max(n, right);
        }

        while (left + delta < right) {
            mid = left + (right - left) / 2;
            if (isAverageValid(nums, mid, k)) {
                left = mid;
            } else {
                right = mid;
            }
        }

        return isAverageValid(nums, right, k) ? right : left;
    }

    private boolean isAverageValid(int[] nums, double avg, int k) {
        double sum = 0, leftSum = 0, leftSumMin = 0;
        for (int i = 0; i < nums.length; i++) {
            // sum is the sum of elements from 0 to i
            sum += nums[i] - avg;
            
            if (i >= k - 1 && sum >= 0) return true;
            if (i >= k) {
                // left sum is the sum of elements from 0 to i-k
                leftSum += nums[i - k] - avg;
                leftSumMin = Math.min(leftSumMin, leftSum);
                // difference here is the max value for a k-length array
                if (sum - leftSumMin >= 0)
                    return true;
            }
        }
        return false;
    }
}
```
