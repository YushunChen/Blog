---
description: ID: 937; medium; 可以完成的题目数量
---
# How Many Problem Can I Accept

{% embed url="https://www.lintcode.com/problem/937/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param n: an integer
     * @param k: an integer
     * @return: how many problem can you accept
     */
    public long canAccept(long n, int k) {
        long left = 0;
        long right = (long) Math.sqrt(2 * n / k);
        while (left + 1 < right) {
            long mid = left + (right - left) / 2;
            if ((findTime(mid, k)) > n) {
                right = mid;
            } else {
                left = mid;
            }
        }
        if (findTime(right, k) <= n) return right;
        return left;
    }

    private long findTime(long i, int k) {
        return k * ((1 + i) * i / 2);
    }
}
```

### Notes

$$
\sum_{i=1}^{x}k \times i \leq n
$$

$$
\frac{x(1+x)}{2} \leq \frac{n}{k} \\ \\
$$

$$
x < \sqrt{x^2+x} \leq \sqrt{\frac{2n}{k}}
$$

The search range is `[0, sqrt(2n/k)]`. Normally, we would set `right` to be `n`, but here it would exceed the time limit since `n` is long.
