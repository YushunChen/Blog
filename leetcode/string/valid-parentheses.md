# Valid Parentheses

{% embed url="https://leetcode.com/problems/valid-parentheses/" %}

## Solution 1

```go
import "fmt"

var m = map[string]int{
    "(": -1,
    "{": -2,
    "[": -3,
    ")": 1,
    "}": 2,
    "]": 3,
}

func isValid(s string) bool {
    for i := 0; i < len(s); i++ {
        j := i+1
        if m[string(s[i])] < 0 {
            for j < len(s) {
                if m[string(s[j])] + m[string(s[i])] == 0 {
                    fmt.Println(m[string(s[j])], m[string(s[i])])
                    break
                } else {
                    j++
                }
                return false
            }
        }
    }
    return true
}
```

