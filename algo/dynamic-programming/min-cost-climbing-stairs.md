---
description: 'ID: 746; easy'
---

# Min Cost Climbing Stairs

{% embed url="https://leetcode.com/problems/min-cost-climbing-stairs" %}

## Solution 1

```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int[] minCost = new int[cost.length + 1];
        for (int i = 2; i < minCost.length; i++) {
            int oneStep = minCost[i - 1] + cost[i - 1];
            int twoStep = minCost[i - 2] + cost[i - 2];
            minCost[i] = Math.min(oneStep, twoStep);
        } 
        return minCost[minCost.length - 1];
    }
}
```

This is the DP equation:

$$
minCost[i] = min(minCost[i-1] + cost[i-1], minCost[i-2], cost[i-2])
$$

For the minimum cost to reach the ith step, we either came from the one-step hop or  from the two-step hop (with their corresponding minimum costs as well).

Time complexity: O(n)

Space complexity: O(n)

## Solution 2

```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int downOne = 0;
        int downTwo = 0;
        for (int i = 2; i < cost.length + 1; i++) {
            int oneStep = downOne + cost[i - 1];
            int twoStep = downTwo + cost[i - 2];
            int tempDownTwo = downOne;
            downOne = Math.min(oneStep, twoStep);
            downTwo = tempDownTwo;
        } 
        return downOne;
    }
}
```

Similarly, we can improve the space complexity by just using variables instead of the whole array. It become a little more abstract now.

`downOne` and `downTwo` represents the minimum cost to reach one step and two steps below the current step that we are taking. Inside the loop, each iteration, `downOne` is after `downTwo`. We calculate the minimum and update `downOne`. Then, `downTwo` is updated to be the old `downOne`.
