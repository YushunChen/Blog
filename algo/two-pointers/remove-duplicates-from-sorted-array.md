---
description: ID: 26: Easy
---
# Remove Duplicates from Sorted Array

{% embed url="https://leetcode.com/problems/remove-duplicates-from-sorted-array/" %}

{% embed url="https://www.lintcode.com/problem/100/" %}

## Solution 1 (Go)

```go
func removeDuplicates(nums []int) int {
    i := 0
    for j:=0; j<len(nums); j++ {
        if nums[i] != nums[j] {
            i++
            nums[i] = nums[j]
        }
    }
    return i+1
}
```

## Solution 2 (Java)

```go
public class Solution {
    /*
     * @param nums: An ineger array
     * @return: An integer
     */
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0)
            return 0;
        int i = 0;
        for (int j = 0; j < nums.length; j++) {
            if (nums[i] != nums[j]) {
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;
    }
}
```

### Notes

* `i` is the writing pointer and `j` is the reading pointer.
* We only change the array in place if the reading pointer encounter some number that is different from the writing pointer.
