---
description: 'ID: 414; easy'
---

# Third Maximum Number

{% embed url="https://leetcode.com/problems/third-maximum-number/" %}

## Solution 1

```go
import "math"

func thirdMax(nums []int) int {
    firstMax, secondMax, thirdMax := math.MinInt64, math.MinInt64, math.MinInt64
    for _, v := range nums {
        if v > firstMax {
            thirdMax = secondMax
            secondMax = firstMax
            firstMax = v
        } else if v > secondMax && v < firstMax {
            thirdMax = secondMax
            secondMax = v
        } else if v > thirdMax && v < secondMax {
            thirdMax = v
        }
    }
    if thirdMax == math.MinInt64 {
        return firstMax
    }
    return thirdMax
}
```

