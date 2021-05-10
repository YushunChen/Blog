---
description: Easy
---

# Two Sum

{% embed url="https://leetcode.com/problems/two-sum/" %}

## 1st Attempt

```go
func twoSum(nums []int, target int) []int {
    var indices []int
    for i := 0; i < len(nums)-1; i++ {
        for j := i+1; j < len(nums) ; j++ {
            if nums[i] + nums[j] == target {
                indices = append(indices, i, j)
            }
        }
    }
    return indices
}
```

## 2nd Attempt

```go
func twoSum(nums []int, target int) []int {
    m := make(map[int]int)
    for i,v := range nums {
        j := target - v
        if _, ok := m[j]; ok {
            return []int{m[j], i}
        }
        m[v] = i
    }
    return nil
}
```



