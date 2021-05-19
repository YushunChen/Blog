---
description: 'ID: 122; easy'
---

# Best Time to Buy and Sell Stock II

{% embed url="https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/" %}

## 1st Solution

```go
func maxProfit(prices []int) int {
    profit := 0
    for i := 1; i < len(prices); i++ {
        diff := prices[i] - prices[i-1]
        if diff > 0 {
            profit += diff
        }
    }
    return profit
}
```

