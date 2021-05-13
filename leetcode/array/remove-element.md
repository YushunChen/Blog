---
description: 'ID: 27; Easy'
---

# Remove Element

{% embed url="https://leetcode.com/problems/remove-element/" %}

## 1st Solution

```go
func removeElement(nums []int, val int) int {
    i := 0
    for j := 0; j < len(nums); j++ {
        if nums[j] != val {
            nums[j], nums[i] = nums[i], nums[j]
            i++
        } 
    }
    return i
}
```

## 2nd Solution

```go
func removeElement(nums []int, val int) int {
    i := 0
    for j := 0; j < len(nums); j++ {
        if nums[j] != val {
            nums[i] = nums[j]
            i++
        } 
    }
    return i
}
```

