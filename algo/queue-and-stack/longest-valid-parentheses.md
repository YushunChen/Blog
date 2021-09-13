---
description: 'ID: 193; medium'
---

# Longest Valid Parentheses

{% embed url="https://www.lintcode.com/problem/193" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param s: a string
     * @return: return a integer
     */
    public int longestValidParentheses(String s) {
        Deque<Integer> stack = new ArrayDeque<>();
        int maxLength = 0;
        int currLength = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                stack.push(i);
            } else {
                if (stack.isEmpty()) {
                    currLength = 0;
                } else {
                    int matchIndex = stack.pop();
                    int matchLength = i - matchIndex + 1;
                    if (stack.isEmpty()) {
                        currLength += matchLength;
                        matchLength = currLength;
                    } else {
                        matchLength = i - stack.peek();
                    }
                    maxLength = Math.max(maxLength, matchLength);
                }
            }
        }
        return maxLength;
    }
}
```

