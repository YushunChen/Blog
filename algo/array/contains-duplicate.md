---
description: ID: 217; easy
---
# Contains Duplicate

{% embed url="https://leetcode.com/problems/contains-duplicate/" %}

## Solution 1

```go
func containsDuplicate(nums []int) bool {
    m := make(map[int]int)
    for _, v := range nums {
        m[v]++
        if m[v] >= 2 {
            return true
        }
    }
    return false
}
```

## Solution 2

```go
func containsDuplicate(nums []int) bool {
    m := make(map[int]bool, len(nums))
	for _, n := range nums {
		if _, found := m[n]; found {
			return true
		}
		m[n] = true
	}
	return false
}
```

{% hint style="info" %}
Booleans take less space
{% endhint %}
