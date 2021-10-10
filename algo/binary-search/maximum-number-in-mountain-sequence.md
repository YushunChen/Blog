---
description: ID: 585; medium; 山脉序列中的最大值
---
# Maximum Number in Mountain Sequence

{% embed url="https://www.lintcode.com/problem/585/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param nums: a mountain sequence which increase firstly and then decrease
     * @return: then mountain top
     */
    public int mountainSequence(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }

        int left = 0, right = nums.length - 1;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid-1] < nums[mid] && nums[mid] > nums[mid+1]) {
                return nums[mid];
            } else if (nums[mid-1] < nums[mid] && nums[mid] < nums[mid+1]) {
                left = mid;
            } else {
                right = mid;
            }
        }

        return Math.max(nums[left], nums[right]);
    }
}
```

