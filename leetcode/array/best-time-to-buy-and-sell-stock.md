---
description: 'ID: 121; easy'
---

# Best Time to Buy and Sell Stock

{% embed url="https://leetcode.com/problems/best-time-to-buy-and-sell-stock/" %}

## Solution 1

```go
func maxProfit(prices []int) int {
    start, profit := prices[0], 0
    for i := 0; i < len(prices); i++ {
        diff := prices[i] - start
        if diff > profit {
            profit = diff
        } else if diff < 0 {
            start = prices[i]
        }
    }
    return profit
}
```



