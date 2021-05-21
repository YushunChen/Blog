---
description: 'ID: 228; easy'
---

# Summary Ranges

{% embed url="https://leetcode.com/problems/summary-ranges/" %}

## Solution 1

```go
import "strconv"

func summaryRanges(nums []int) []string {
    res := make([]string, 0)
    if len(nums) == 1 {
        res = append(res, strconv.Itoa(nums[0]))
        return res
    }
    inRange, start, end := false, 0, 0
    for i := 0; i < len(nums); i++ {
        if !inRange {
            if i == len(nums)-1 {
                res = append(res, strconv.Itoa(nums[i]))
                break
            }
            if nums[i] + 1 == nums[i+1] {
                inRange, start, end = true, nums[i], nums[i+1]
            } else {
                res = append(res, strconv.Itoa(nums[i]))
            }
        } else {
            if i == len(nums)-1 {
                res = append(res, strconv.Itoa(start) + "->" + strconv.Itoa(end))
                break
            }
            if nums[i] + 1 == nums[i+1] {
                end = nums[i+1]
            } else {
                res = append(res, strconv.Itoa(start) + "->" + strconv.Itoa(end))
                inRange = false
            }
        }
        
    }
    return res
}
```

