---
description: 'ID: 35; easy'
---

# Search Insert Position

{% embed url="https://leetcode.com/problems/search-insert-position/" %}

## 1st Solution

```go
func searchInsert(nums []int, target int) int {
    low, high := 0, len(nums)-1
    for low <= high {
        mid := (low+high)/2
        if nums[mid] == target {
            return mid
        } else if nums[mid] > target {
            high = mid - 1
        } else if nums[mid] < target {
            if (mid == len(nums)-1) || (target < nums[mid+1]) {
                return mid + 1
            }
            low = mid + 1
        }
    }
    return 0
}
```

