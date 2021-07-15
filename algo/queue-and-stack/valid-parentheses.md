---
description: 'ID: 20; easy'
---

# Valid Parentheses

{% embed url="https://leetcode.com/problems/valid-parentheses/" %}

{% embed url="https://www.lintcode.com/problem/423/" %}

## Solution 1 \(Go\)

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

## Solution 2 \(Java\)

```go
public class Solution {
    /**
     * @param s: A string
     * @return: whether the string is a valid parentheses
     */
    public boolean isValidParentheses(String s) {
        if (s == null || s.length() == 0)
            return true;
        char[] arr = s.toCharArray();
        Deque<Character> stack = new ArrayDeque<>(); 
        for (char c : arr) {
            if (c == '(' || c == '[' || c == '{') {
                stack.push(c);
            } else {
                if (stack.isEmpty())
                    return false;
                if (c == ')' && stack.pop() != '(')
                    return false;
                if (c == ']' && stack.pop() != '[')
                    return false;
                if (c == '}' && stack.pop() != '{')
                    return false;
            }
        }
        return stack.isEmpty();
    }
}
```

