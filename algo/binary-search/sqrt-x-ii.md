---
description: ID: 586; medium; 对x开根II
---
# Sqrt(x) II

{% embed url="https://www.lintcode.com/problem/586/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param x: a double
     * @return: the square root of x
     */
    public double sqrt(double x) {
        double left = 0;
        double right = Math.max(x, 1.0);
        double delta = 1e-12;
        while (left + delta < right) {
            double mid = left + (right - left) / 2;
            if (mid * mid <= x) {
                left = mid;
            } else {
                right = mid;
            }
        }
        return left;

    }
}
```

### Notes

* Discuss the cases when `x` is greater than 1 and `x` is less than 1.
* 12 decimal places can be achieved by setting the `delta`/difference between left and right to be `1e-12`.
