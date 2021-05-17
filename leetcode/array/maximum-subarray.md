---
description: 'ID: 35; easy'
---

# Maximum Subarray

{% embed url="https://leetcode.com/problems/maximum-subarray/" %}

## 1st Solution

```go
func maxSubArray(nums []int) int {
    if len(nums) == 1 {
        return nums[0]
    }
    max, result := nums[0], 0
    for i := 0; i < len(nums); i++ {
        result += nums[i]
        // only update result when it can be increased
        if result > max {
            max = result
        }
        if result < 0 {
            result = 0
        }
    }
    return max
}
```

## 2nd Solution

```go
func Max(x, y int) int {
    if x < y {
        return y
    }
    return x
}

func maxSubArray(nums []int) int {
    if len(nums) == 1 {
        return nums[0]
    }
    dp, result := make([]int, len(nums)), nums[0]
    // base case
    dp[0] = nums[0]
    // recursive relation
    for i := 1; i < len(nums); i++ {
        dp[i] = Max(dp[i-1] + nums[i], nums[i])
        result = Max(result, dp[i])
    }
    return result
}
```

