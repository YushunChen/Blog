---
description: ID: 366; naive; 斐波纳契数列
---
# Fibonacci

{% embed url="https://www.lintcode.com/problem/366/" %}

## "Solution 1" (Java)

```java
public class Solution {
    /**
     * @param n: an integer
     * @return: an ineger f(n)
     */
    public int fibonacci(int n) {
        if (n <= 1) return 0;
        if (n == 2) return 1;
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
}
```

### Notes

* Classical recursion example
* This actually will not pass the test on LintCode (test a relatively large Fibonacci number say the 50th).
* Time complexity: `O(2^n)`, extremely bad exponential runtime.
* Space complexity: `O(1)`, excluding stack space (`O(n)`).

## Solution 2 (Java)

```java
public class Solution {
    /**
     * @param n: an integer
     * @return: an ineger f(n)
     */
    public int fibonacci(int n) {
        int[] memo = new int[n + 1];
        return fibHelper(n, memo);
    }

    private int fibHelper(int n, int[] memo) {
        if (n <= 1) return 0;
        if (n == 2) return 1;
        if (memo[n] > 0) return memo[n];
        memo[n] = fibHelper(n - 1, memo) + fibHelper(n - 2, memo);
        return memo[n];
    }
}
```

### Notes

* This solution uses an array to store the Fibonacci values by the concept of **memoization**. 
* Time complexity: `O(n)`
* Space complexity: `O(n)`

## Solution 3 (Java)

```java
public class Solution {
    /**
     * @param n: an integer
     * @return: an ineger f(n)
     */
    public int fibonacci(int n) {
        int n1 = 0, n2 = 1, sum = 0;
        for (int i = 1; i < n; i++) {
            sum = n1 + n2;
            n1 = n2;
            n2 = sum;
        }
        return n1;
    }
}
```

### Notes

* This solution also uses the idea of **memoization**, but it uses a constant number of variables to only store the most important information (current 3 numbers).
* `n1`, `n2`, `sum `are the current two numbers and the previous sum of the two numbers.
* Time complexity: `O(n)`
* Space complexity: `O(1)`

## Solution 4 (Java)

```java
public class Solution {
    /**
     * @param n: an integer
     * @return: an ineger f(n)
     */
    public int fibonacci(int n) {
        int[] fib = new int[]{0, 1, 1};
        for (int i = 3; i < n; i++) {
            fib[i % 3] = fib[(i-1) % 3] + fib[(i-2) % 3];
        }
        return fib[(n-1) % 3];
    }
}
```

### Notes

* This solution is similar to [Solution 2](fibonacci.md#solution-2-java) by using a length-3 array to store the 3 important numbers.
* It is also somewhat different because the third element of the array is indeed the current sum of the first and second elements.
* Time complexity: `O(n)`
* Space complexity: `O(1)`

## Solution 5 (Java)

```java
public class Solution {
    /**
     * @param n: an integer
     * @return: an ineger f(n)
     */
    public int fibonacci(int n) {
        int[][] fib = new int[][] { { 1, 1 }, { 1, 0 } };
        if (n <= 1) return 0;
        power(fib, n);
        return fib[0][0];
    }

    private void power(int[][] fib, int n) {
        int[][] fibCopy = new int[][] { { 1, 1 }, { 1, 0 } };
        for (int i = 0; i < n - 3; i++) {
            matrixMul(fib, fibCopy);
        }
    }

    private void matrixMul(int[][] fib, int[][] fibCopy) {
        int x = fib[0][0] * fibCopy[0][0] + fib[0][1] * fibCopy[1][0];
        int y = fib[0][0] * fibCopy[0][1] + fib[0][1] * fibCopy[1][1];
        int z = fib[1][0] * fibCopy[0][0] + fib[1][1] * fibCopy[1][0];
        int w = fib[1][0] * fibCopy[0][1] + fib[1][1] * fibCopy[1][1];

        fib[0][0] = x;
        fib[0][1] = y;
        fib[1][0] = z;
        fib[1][1] = w;
    }
}
```

### Notes

$$
\begin{pmatrix}
1 & 1 \\
1 & 0
\end{pmatrix}^n =
\begin{pmatrix}
F_{n+1} & F_n \\
F_n & F_{n-1}
\end{pmatrix}
$$

* By the above mathematical rule of Fibonacci numbers, we have this solution.
* Note that the loop does not run for `n = 1, 2, 3` nor any non-positive numbers. So it starts with `n = 4 `in the code, but n is actually 2 in the formula and the top-left element would be F3, which is the correct result for the input `n = 4` in the code.
* Time complexity: `O(n)`
* Space complexity: `O(1)`

## Solution 6 (Java)

```java
public class Solution {
    /**
     * @param n: an integer
     * @return: an ineger f(n)
     */
    public int fibonacci(int n) {
        int[][] fib = new int[][] { { 1, 1 }, { 1, 0 } };
        if (n <= 1) return 0;
        power(fib, n - 2);
        return fib[0][0];
    }

    private void power(int[][] fib, int n) {
        if (n == 0 || n == 1) return;
        int[][] fibCopy = new int[][] { { 1, 1 }, { 1, 0 } };
        power(fib, n / 2);
        matrixMul(fib, fib);

        if (n % 2 != 0) matrixMul(fib, fibCopy);
    }

    private void matrixMul(int[][] fib, int[][] fibCopy) {
        int x = fib[0][0] * fibCopy[0][0] + fib[0][1] * fibCopy[1][0];
        int y = fib[0][0] * fibCopy[0][1] + fib[0][1] * fibCopy[1][1];
        int z = fib[1][0] * fibCopy[0][0] + fib[1][1] * fibCopy[1][0];
        int w = fib[1][0] * fibCopy[0][1] + fib[1][1] * fibCopy[1][1];

        fib[0][0] = x;
        fib[0][1] = y;
        fib[1][0] = z;
        fib[1][1] = w;
    }
}
```

### Notes

* Using the same idea in [Solution 5](fibonacci.md#solution-5-java), we optimize the `power` function by using `divide and conquer`. This idea is also illustrated in this [Pow(x, n)](../math/pow-x-n.md) problem.
* Time complexity: `O(log n)`
* Space complexity: `O(1)`

This solution can also be extended by deriving a recursive relation from the matrix multiplication. The formula/relation is: 

* When n is even and k = n / 2,

$$
F(n) = [2 \times F(k -1) + F(k)] \times F(k)
$$

* When n is even and k = (n+1) / 2,

$$
F(n) = F(k) \times F(k) + F(k-1) \times F(k-1)
$$

* The derivation is shown here:

{% embed url="https://en.wikipedia.org/wiki/Fibonacci_number#Matrix_form" %}

* This extension would have the same time and space complexity as done in code above. The reason is that this is still essentially **divide and conquer** where `k` is half of `n` each time.

## Solution 7 (Java)

```java
public class Solution {
    /**
     * @param n: an integer
     * @return: an ineger f(n)
     */
    public int fibonacci(int n) {
        double phi = (1 + Math.sqrt(5)) / 2;
        return (int) Math.round(Math.pow(phi, --n) / Math.sqrt(5));
    }
}
```

### Notes

$$
F(n) = \frac{1}{\sqrt{5}}[(\frac{1+\sqrt{5}}{2})^n - (\frac{1-\sqrt{5}}{2})^n]
$$

* This solution uses the mathematical formula for calculation (not the recursive relation).
* Note that `n--` because the problem is 1-indexed. 
* Time complexity: `O(log n)` with the assumption that `Math.pow` takes `log n` time.
* Space complexity: `O(1)`.
