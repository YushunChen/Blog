---
description: ID: 169; easy
---
# Majority Element

{% embed url="https://leetcode.com/problems/majority-element/" %}

## Solution 1

```go
func majorityElement(nums []int) int {
    m := make(map[int]int)
    for _,v := range nums {
        m[v]++
        if m[v] > len(nums)/2 {
            return v
        }
    }
    return -1
}
```

## Solution 2

```go
func majorityElement(nums []int) int {
    candidate, count := 0, 0
    for _,v := range nums {
        if count == 0 {
            candidate = v
        }
        if v == candidate {
            count++
        } else {
            count--
        }
    }
    return candidate
    
}
```

{% hint style="info" %}
Boyer-Moore Voting Algorithm
{% endhint %}
