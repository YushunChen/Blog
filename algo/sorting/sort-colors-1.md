---
description: 'ID: 75; medium'
---

# Sort Colors

{% embed url="https://leetcode.com/problems/sort-colors/" %}

{% embed url="https://www.lintcode.com/problem/148/" %}

## Solution 1 \(Go\)

```go
func sortColors(nums []int)  {
    j := 0
    for i := 0; i < len(nums); i++ {
        if nums[i] == 0 {
            nums[i], nums[j] = nums[j], nums[i]
            j++
        }
    }
    
    for i := j; i < len(nums); i++ {
        if nums[i] == 1 {
            nums[i], nums[j] = nums[j], nums[i]
            j++
        }
    }
}
```

## Solution 2 \(Go\)

```go
func sortColors(nums []int)  {
    i, j, k := 0, 0, len(nums)-1
    for j <= k {
        if nums[j] == 0 {
            nums[i], nums[j] = nums[j], nums[i]
            i++
            j++
        } else if nums[j] == 1 {
            j++
        } else {
            nums[j], nums[k] = nums[k], nums[j]
            k--
        }
    }
}
```

`[0, i)`: the interval containing all 0's

`[i, j)`: the interval containing all 1's

`[j ,k)`: the interval to be explored

`[k ,len(nums))`: the interval containing all 2's

## Solution 3 \(Java\)

```java
public class Solution {
    /**
     * @param nums: A list of integer which is 0, 1 or 2 
     * @return: nothing
     */
    public void sortColors(int[] nums) {
        quickSort(nums, 1);
        quickSort(nums, 2);
    }

    private void quickSort(int[] nums, int k) {
        if (nums == null) return;
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
                nums[i] = nums[j];
                nums[j] = temp;
            }
        }
    }
}
```

### Notes

* **Quick sort**

