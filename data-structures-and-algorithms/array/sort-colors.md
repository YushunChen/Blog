---
description: 'ID: 75; medium'
---

# Sort Colors

{% embed url="https://leetcode.com/problems/sort-colors/" %}

## Solution 1

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

## Solution 2

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

