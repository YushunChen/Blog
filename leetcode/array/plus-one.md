---
description: 'ID: 66; Easy'
---

# Plus One

{% embed url="https://leetcode.com/problems/plus-one/" %}

## 1st Solution

```go
func plusOne(digits []int) []int {
    for i := len(digits)-1; i >= 0; i-- {
        digits[i]++
        if digits[i] != 10 {
            return digits
        }
        digits[i] = 0
    }
    digits[0] = 1
    digits = append(digits, 0)
    return digits
}
```

