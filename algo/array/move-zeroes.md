---
description: ID: 283; easy
---
# Move Zeroes

{% embed url="https://leetcode.com/problems/move-zeroes/" %}

## Solution 1

```go
func moveZeroes(nums []int)  {
    for i := 0; i < len(nums)-1; i++ {
        j := i
        if nums[i] == 0 {
            for j++; j < len(nums)-1 && nums[j] == 0; j++ {}
            nums[i], nums[j] = nums[j], nums[i]
        }
    }
}
```

## Solution 2

```go
func moveZeroes(nums []int)  {
    j := 0
    for i := 0; i < len(nums); i++ {
        if nums[i] != 0 {
            if i != j {
                nums[i], nums[j] = nums[j], nums[i]
                j++
            } else {
                j++
            }
        }
    }
}
```
