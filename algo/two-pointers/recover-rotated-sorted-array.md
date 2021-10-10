---
description: ID: 39; easy
---
# Recover Rotated Sorted Array

{% embed url="https://www.lintcode.com/problem/39/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param nums: An integer array
     * @return: nothing
     */
    public void recoverRotatedSortedArray(List<Integer> nums) {
        if (nums == null || nums.size() == 0)
            return;
        for (int i = 0; i < nums.size() - 1; i++) {
            if (nums.get(i) > nums.get(i + 1)) {
                rotate(nums, 0, i);
                rotate(nums, i + 1, nums.size() - 1);
                rotate(nums, 0, nums.size() - 1);
                return;
            }
        }
    }

    private void rotate(List<Integer> nums, int left, int right) {
        while (left < right) {
            int temp = nums.get(left);
            nums.set(left, nums.get(right));
            nums.set(right, temp);
            left++;
            right--;
        }
        
    }
}
```
