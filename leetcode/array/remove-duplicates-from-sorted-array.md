---
description: 'ID: 26: Easy'
---

# Remove Duplicates from Sorted Array

{% embed url="https://leetcode.com/problems/remove-duplicates-from-sorted-array/" %}

## 1st Attempt

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



