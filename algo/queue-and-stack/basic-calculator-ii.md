---
description: ID: 980; medium
---
# Basic Calculator II

{% embed url="https://www.lintcode.com/problem/980/description" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param s: the given expression
     * @return: the result of expression
     */
    public int calculate(String s) {
        if (s == null || s.length() == 0)
            return 0;
        
        int num = 0;
        char op = '+';
        Deque<Integer> stack = new ArrayDeque<>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (Character.isDigit(c)) {
                num = num * 10 + c - '0';
            }
            if (c != ' ' && !Character.isDigit(c) || i == s.length() - 1) {
                if (op == '+') stack.push(num);
                if (op == '-') stack.push(-num);
                if (op == '*') stack.push(stack.pop() * num);
                if (op == '/') stack.push(stack.pop() / num);
                num = 0;
                op = c;
            }
        }
        int res = 0;
        for (int n : stack) {
            res += n;
        }
        return res;
    }
}

// "3+22" num = 2, op = +; c = '2'
// stack: [3, 22]
```
