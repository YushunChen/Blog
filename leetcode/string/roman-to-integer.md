---
description: 'ID: 3; easy'
---

# Roman to Integer

{% embed url="https://leetcode.com/problems/roman-to-integer/" %}

## Solution 1

```go
var m = map[string]int{
    "I": 1,
    "V": 5,
    "X": 10,
    "L": 50,
    "C": 100,
    "D": 500,
    "M": 1000,
}

func romanToInt(s string) int {
    lastNum, result := 0, 0
    for i := len(s)-1; i >= 0; i-- {
        currLetter := s[i]
        currNum := m[string(currLetter)]
        if currNum >= lastNum {
            result += currNum
        } else {
            result -= currNum
        }
        lastNum = currNum
    }
    return result
}
```

