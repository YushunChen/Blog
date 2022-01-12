---
description: 'ID: 1137; easy'
---

# N-th Tribonacci Number



{% embed url="https://leetcode.com/problems/n-th-tribonacci-number" %}

## Solution 1

```java
class Solution {
    public int tribonacci(int n) {
        if (n <= 1) return n;
        if (n == 2) return 1;
        
        int a = 0, b = 1, c = 1, d = 2;
        
        for (int i = 4; i < n + 1; i++) {
            a = b;
            b = c;
            c = d;
            d = a + b + c;
        }
        return d;
    }
}

// a b c d
//   a b c d
//     a b c d
//       a b c d
// 0 1 1 2 4 7 13
```

This is the same bottom-up approach used in [Fibonacci Number](fibonacci-number.md#solution-3). The only difference here is that we use 4 variables to keep the results.
