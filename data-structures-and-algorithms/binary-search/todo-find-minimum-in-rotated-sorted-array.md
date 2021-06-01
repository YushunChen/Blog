---
description: 'ID: 159; medium; 寻找旋转排序数组中的最小值'
---

# Find Minimum in Rotated Sorted Array

{% embed url="https://www.lintcode.com/problem/159/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param nums: a rotated sorted array
     * @return: the minimum number in the array
     */
    public int findMin(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        int left = 0, right = nums.length - 1;
        int target = nums[nums.length - 1];

        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] >= target) {
                left = mid;
            } else {
                right = mid;
            }
        }

        return Math.min(nums[left], nums[right]);
    }
}
```

### Ideas

* We use the last element as the target since we lack a target for the binary search. The reason is that we can reduce the range that contains the minimum number using this target. 
* Also, note that the array may not be rotated at all. 

