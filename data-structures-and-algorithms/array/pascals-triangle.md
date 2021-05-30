---
description: 'ID: 118; easy'
---

# Pascal's Triangle

{% embed url="https://leetcode.com/problems/pascals-triangle/" %}

## Solution 1

```go
func generate(numRows int) [][]int {
    res := make([][]int, numRows)
    res[0] = []int{1}
    if numRows == 1 {
        return res
    }
    res[1] = []int{1, 1}
    if numRows == 2 {
        return res
    }
    for i := 2; i < numRows; i++ {
        middle := make([]int, 0)
        for j := 0; j < len(res[i-1])-1; j++ {
            middle = append(middle, res[i-1][j] + res[i-1][j+1])
        }
        res[i] = make([]int, 0)
        res[i] = append(res[i], 1)
        res[i] = append(res[i], middle...)
        res[i] = append(res[i], 1)
    }
    return res
}
```



