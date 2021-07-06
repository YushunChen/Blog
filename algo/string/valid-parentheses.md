---
description: 'ID: 20; easy'
---

# Valid Parentheses

{% embed url="https://leetcode.com/problems/valid-parentheses/" %}

## Solution 1

```go
func isValid(s string) bool {
    stack := make([]rune, 0)
    for _,v := range s {
        if v == '(' || v == '[' || v == '{' {
            stack = append(stack, v)
        } else if (v == ')' && len(stack) > 0 && stack[len(stack)-1] == '(') ||
            (v == ']' && len(stack) > 0 && stack[len(stack)-1] == '[') ||
            (v == '}' && len(stack) > 0 && stack[len(stack)-1] == '{') {
                stack = stack[:len(stack)-1]
        } else {
            return false
        }
    }
    return len(stack) == 0
}
```

