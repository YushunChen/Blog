---
description: ID: 31; medium
---
# Partition Array

{% embed url="https://www.lintcode.com/problem/31/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param nums: The integer array you should partition
     * @param k: An integer
     * @return: The index after partition
     */
    public int partitionArray(int[] nums, int k) {
        if (nums == null) return 0;

        int i = 0, j = nums.length - 1;
        while (i <= j) {
            while (i <= j && nums[i] < k) {
                i++;
            }
            while (i <= j && nums[j] >= k) {
                j--;
            }
            if (i <= j) {
                int temp = nums[i];
                nums[i++] = nums[j];
                nums[j--] = temp;
            }
        }
        return i;
    }
}
```

### Notes

* **Quick sort**
