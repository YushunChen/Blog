---
description: 'ID: 70; easy'
---

# Climbing Stairs

{% embed url="https://leetcode.com/problems/climbing-stairs" %}

## Solution 1

```java
class Solution {
    public int climbStairs(int n) {
        if (n <= 2) return n;
        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        
        for (int i = 3; i < n + 1; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
}
```

The DP function is:

$$
dp[i] = dp[i-1] + dp[i-2]
$$

`dp[i]` stands for the number of ways to reach the ith step. This number should be equal to the number of ways to reach the (i-1)th step plus the number of ways to reach the (i-2)th step. The reason is that one can only take 1 or 2 steps, so the ith step either comes from the (i-1)th step or the (i-2)th step.

Time complexity: `O(n)`

Space complexity: `O(n)`

## Solution 2

```java
class Solution {
    public int climbStairs(int n) {
        if (n <= 2) return n;
        int a = 1, b = 2, c = 3;
        for (int i = 0; i < n - 3; i++) {
            a = b;
            b = c;
            c = a + b;
        }
        return c;
    }
}

// a b c
//   a b c
//     a b c
// 1 2 3 5 8
```

It is not hard to tell that this DP function resembles the Fibonacci Number function. Then, we can use what we have in the [Fibonacci Number](fibonacci-number.md#solution-3) problem (use 3 variables to dynamically keep the results) to solve this problem.
