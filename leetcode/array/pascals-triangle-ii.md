---
description: 'ID: 119; easy'
---

# Pascal's Triangle II

{% embed url="https://leetcode.com/problems/pascals-triangle-ii/" %}

## 1st Solution

```go
func getRow(rowIndex int) []int {
    res := make([]int, rowIndex + 1)
    res[0] = 1
    for i := 1; i < rowIndex+1; i++ {
        res[i] = res[i-1] * (rowIndex-i+1) / i
    }
    return res
}
```

$$
{n\choose{m}}={n\choose{m-1}} \times \frac{n-m+1}{m}
$$



