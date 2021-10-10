---
description: ID: 50; medium
---
# Pow(x, n)

{% embed url="https://leetcode.com/problems/powx-n/" %}

## Solution 1

```go
func myPow(x float64, n int) float64 {
    if n == 0 {
        return 1
    }
    if n == 1 {
        return x
    }
    if n == -1 {
        return 1/x
    }
    // divide and conquer
    half := myPow(x, n / 2)
    // even case
    if n % 2 == 0 {
        return half * half
    } else if n > 0 {   // odd positive case
        return half * half * x
    } else {            // odd negative case
        return half * half * 1/x
    }
}
```
