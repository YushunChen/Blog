---
description: ID: 268; easy
---
# Missing Number

{% embed url="https://leetcode.com/problems/missing-number/" %}

## Solution 1

```go
func missingNumber(nums []int) int {
    numsSum, n := 0, len(nums)
    for _,v := range nums {
        numsSum += v
    }
    rangeSum := n*(n+1) / 2
    return rangeSum - numsSum
}
```

The thought process here is easy, compared to solution 2. We are given the `nums` array with one element missing from the range `[0, n]`. Since the numbers are distinct, the difference between the sum of the `nums` array and the sum of all numbers in the range `[0, n]` is actually the missing number.

The rangeSum uses the formula for summing arithmetic sequences:

$$
1+2+\cdots+n = \frac{(1+n)\times n}{2}
$$

## Solution 2

```go
func missingNumber(nums []int) int {
    xor, i := 0, 0
    for ; i < len(nums); i++ {
        xor = xor ^ i ^ nums[i]
    }
    return xor ^ i
}
```

{% hint style="info" %}
Bit manipulation. Note that XOR returns 1 if and only if the bits differ.
{% endhint %}

We use the properties that `X ^ X = 0` and `X ^ 0 = X`. Consider the following example, we have the array `[3, 0, 1]`, `n = 3` in this case, and we are missing 2. 

The important thing to notice here is that if we have every number in `[0, n]`, then taking the `XOR` results of all the numbers should give us a 0. For this example,

The array `[3, 0, 1, 2]` contains every number in `[0, 3]`, and

```bash
0 ^ 0 ^ 3 ^ 1 ^ 0 ^ 2 ^ 1 ^ 3 ^ 2 = 0    // order doesn't matter
```

For the array with a missing element 2: `[3, 0, 1]`, we have

```bash
0 ^ 0 ^ 3 ^ 1 ^ 0 ^ 2 ^ 1 = 0 ^ 3 ^ 2 = 3 ^ 2
```

The result here is actually 3 (i.e., n) and 2 (the missing element) because the difference between \[0, n-1] and \[0, n] is n and 2 has nothing to cancel itself with. Therefore, taking this result and XOR it with n gives us the final result:

```bash
3 ^ 2 ^ 3 = 2
```
