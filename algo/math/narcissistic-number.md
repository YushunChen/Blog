---
description: 'ID: 147; easy'
---

# Narcissistic Number

{% embed url="https://www.lintcode.com/problem/147/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param n: The number of digits
     * @return: All narcissistic numbers with n digits
     */
    public List<Integer> getNarcissisticNumbers(int n) {
        List<Integer> res = new ArrayList<>();
        if (n == 0) return res;
        int low = (int) Math.pow(10, n - 1);
        int high = (int) Math.pow(10, n);
        if (n == 1) low = 0;
        
        for (int i = low; i < high; i++) {
            int j = i;
            int sum = 0;
            while (j > 0) {
                sum += Math.pow(j % 10, n);
                j /= 10;
            }
            if (sum == i) res.add(i);
        }
        return res;
    }
}
```

