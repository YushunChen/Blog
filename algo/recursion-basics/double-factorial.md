---
description: ID: 771; easy; 二阶阶乘
---
# Double Factorial

{% embed url="https://www.lintcode.com/problem/771/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param n: the given number
     * @return:  the double factorial of the number
     */
    public long doubleFactorial(int n) {
        if (n == 0 || n == 1) return 1;
        return (long)n * doubleFactorial(n - 2);
    }
}
```

### Notes

* By definition of double factorial, the result is immediate.
