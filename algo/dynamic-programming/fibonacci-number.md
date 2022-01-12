---
description: 'ID: 509; easy'
---

# Fibonacci Number

{% embed url="https://leetcode.com/problems/fibonacci-number" %}

## Solution 1

```java
class Solution {
    public int fib(int n) {
        if (n == 0) return 0;
        if (n == 1) return 1;
        
        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;
        for (int i = 2; i < n + 1; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        
        return dp[n];
    }
}
```

This the bottom-up tabulation approach. We start from the very "bottom" and add up the numbers until `n`.

Time complexity: `O(n)`

Space complexity: `O(n)`

## Solution 2

```java
class Solution {
    private Map<Integer, Integer> map = new HashMap<>();
    
    public int fib(int n) {
        if (n <= 1) return n;
        map.putIfAbsent(0, 0);
        map.putIfAbsent(1, 1);
        if (map.containsKey(n)) {
            return map.get(n);
        }
        map.put(n, fib(n - 1) + fib(n - 2));
        return map.get(n);
}
```

This is the top-down memoization approach. We use a hash table to achieve memoization.

Time complexity: `O(n)`

Space complexity: `O(n)`

## Solution 3

```java
class Solution {
    public int fib(int n) {
        if (n <= 1) return n;
        int x = 0, y = 1, z = 1;
        
        for (int i = 3; i < n + 1; i++) {
            x = y;
            y = z;
            z = x + y;
        }
        return z;
    }
}
// x y z
//   x y z
// 0 1 1 2 3 5 8
```

This is the bottom-up approach without using an array to keep the results. Instead, we only use three variables to keep the progress.

Time complexity: `O(n)`

Space complexity: `O(1)`
