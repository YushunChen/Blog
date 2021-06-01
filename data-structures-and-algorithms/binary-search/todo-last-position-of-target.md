---
description: 'ID: 458; easy; 目标最后位置'
---

# Last Position of Target

{% embed url="https://www.lintcode.com/problem/458/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param nums: An integer array sorted in ascending order
     * @param target: An integer
     * @return: An integer
     */
    public int lastPosition(int[] nums, int target) {
        if (nums == null || nums.length == 0)  {
            return -1;
        }

        int left = 0;
        int right = nums.length - 1;

        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] <= target) {
                left = mid;
            } else {
                right = mid;
            }
        }

        if (nums[right] == target) return right;
        if (nums[left] == target) return left;
        return -1;
    }
}
```

