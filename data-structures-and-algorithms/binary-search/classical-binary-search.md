---
description: 'ID: 457; easy; 经典二分查找问题'
---

# Classical Binary Search

{% embed url="https://www.lintcode.com/problem/457/." %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param nums: An integer array sorted in ascending order
     * @param target: An integer
     * @return: An integer
     */
    public int findPosition(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        int left = 0;
        int right = nums.length - 1;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
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

* The loop condition `left + 1 < right` will guarantee that we end up with two indices that are next to each other. Then, we return either of them at the end.
* The middle point `mid` is calculated using `left + (right - left) / 2` instead of `(left + right) / 2` in order to prevent integer overflow, which the addition may have while the subtraction will not.

