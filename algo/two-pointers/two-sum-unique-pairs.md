---
description: 'ID: 587; medium'
---

# Two Sum - Unique pairs

{% embed url="https://www.lintcode.com/problem/587/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param nums: an array of integer
     * @param target: An integer
     * @return: An integer
     */
    public int twoSum6(int[] nums, int target) {
        if (nums == null || nums.length == 0)
            return 0;
        int left = 0, right = nums.length - 1, ans = 0;
        Arrays.sort(nums);
        while (left < right) {
            while (left < right && nums[left] + nums[right] < target) {
                left++;
            }
            if (left != right && nums[left] + nums[right] == target) {
                ans++;
                while (left < right && nums[right] == nums[right - 1]) {
                    right--;
                }
            }
            right--;
        }
        return ans;
    }
}
```

