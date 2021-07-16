---
description: 'ID: 12; medium'
---

# Min Stack

{% embed url="https://www.lintcode.com/problem/12/" %}

## Solution 1 \(Java\)

```java
public class MinStack {

    private Deque<Integer> stack;
    private Deque<Integer> minStack;

    public MinStack() {
        stack = new ArrayDeque<>();
        minStack = new ArrayDeque<>();
    }

    /*
     * @param number: An integer
     * @return: nothing
     */
    public void push(int number) {
        stack.push(number);
        if (minStack.isEmpty()) {
            minStack.push(number);
        } else {
            int currMin = minStack.peek();
            minStack.push(Math.min(currMin, number));
        }
            
    }

    /*
     * @return: An integer
     */
    public int pop() {
        minStack.pop();
        return stack.pop();
    }

    /*
     * @return: An integer
     */
    public int min() {
        return minStack.peek();
    }
}

// stack:    [1,2,3]
// minStack: [1,1,1]
```

