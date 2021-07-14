---
description: 'ID: 608; medium'
---

# Two Sum II - Input array is sorted

{% embed url="https://www.lintcode.com/problem/608/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param nums: an array of Integer
     * @param target: target = nums[index1] + nums[index2]
     * @return: [index1 + 1, index2 + 1] (index1 < index2)
     */
    public int[] twoSum(int[] nums, int target) {
        if (nums == null || nums.length == 0)
            return null;
        int left = 0, right = nums.length - 1;
        while (left < right) {
            if (nums[left] + nums[right] == target)
                return new int[]{left + 1, right + 1};
            else if (nums[left] + nums[right] < target)
                left++;
            else
                right--;
        }
        return null;
    }
}
```

### Notes

* Here we sufficiently use the condition that the array is sorted.

