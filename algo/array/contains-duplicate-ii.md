---
description: ID: 219; easy
---
# Contains Duplicate II

{% embed url="https://leetcode.com/problems/contains-duplicate-ii/" %}

## Solution 1

```go
func containsNearbyDuplicate(nums []int, k int) bool {
    m := make(map[int]int)
    for i,v := range nums {
        if _, found := m[v]; found {
            if i - m[v] <= k {
                return true
            }
        }
        m[v] = i
    }
    return false
}
```

## Solution 2

```go
func containsNearbyDuplicate(nums []int, k int) bool {
    m := make(map[int]bool, len(nums))
    for i,v := range nums {
        if _, found := m[v]; found {
            return true
        }
        m[v] = true
        if len(m) == k+1 {
            delete(m, nums[i-k])
        }
    }
    return false
}
```

{% hint style="info" %}
Maintain a map of k elements
{% endhint %}
