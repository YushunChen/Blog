---
description: 'ID: 424; medium'
---

# Evaluate Reverse Polish Notation

{% embed url="https://www.lintcode.com/problem/424/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param tokens: The Reverse Polish Notation
     * @return: the value
     */
    public int evalRPN(String[] tokens) {
        Deque<Integer> stack = new ArrayDeque<>();
        String operators = "+-*/";
        for (String s : tokens) {
            if (operators.contains(s)) {
                int num1 = stack.pop();
                int num2 = stack.pop();
                if (s.equals("+")) stack.push(num1 + num2);
                if (s.equals("-")) stack.push(num2 - num1); 
                if (s.equals("*")) stack.push(num1 * num2);
                if (s.equals("/")) stack.push(num2 / num1);
            } else {
                stack.push(Integer.parseInt(s));
            }
        }
        return stack.pop();
    }
}
```

### Notes

* Be careful about the order of the two numbers for subtracting and dividing.

