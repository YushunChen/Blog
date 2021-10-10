---
description: ID: 119; easy
---
# Pascal's Triangle II

{% embed url="https://leetcode.com/problems/pascals-triangle-ii/" %}

## Solution 1

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

```java
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> ans = new ArrayList<>();
        ans.add(1);
        long curElement = 1;
        for (int i = 1; i <= rowIndex; i++) {
            curElement = curElement * (rowIndex-i+1) / i;
            ans.add((int)curElement);
        }
        return ans;
    }
}
```
