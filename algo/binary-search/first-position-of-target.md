---
description: ID: 14; easy; 二分查找
---
# First Position of Target

{% embed url="https://www.lintcode.com/problem/14/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param nums: The integer array.
     * @param target: Target to find.
     * @return: The first position of target. Position starts from 0.
     */
    public int binarySearch(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }

        int left = 0;
        int right = nums.length - 1;

        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] < target) {
                left = mid;
            } else {
                right = mid;
            }
        }

        if (nums[left] == target) return left;
        if (nums[right] == target) return right;
        return -1;
    }
}
```

### Notes

* This is very similar to the classical binary search. However, we do not return mid when we immediately find a value because we are not sure if it is the first position. So, we only reduce the range. Eventually we have the range `[left, right]` that contains the target and we return `left` if possible to ensure that it is the first position of target.
