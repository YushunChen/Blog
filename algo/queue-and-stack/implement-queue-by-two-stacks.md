---
description: 'ID: 40; medium'
---

# Implement Queue by Two Stacks

{% embed url="https://www.lintcode.com/problem/40/" %}

## Solution 1 \(Java\)

```java
public class MyQueue {

    private Deque<Integer> s1 = new ArrayDeque<>();
    private Deque<Integer> s2 = new ArrayDeque<>();

    public MyQueue() {

    }

    /*
     * @param element: An integer
     * @return: nothing
     */
    public void push(int element) {
        s1.push(element);
    }

    /*
     * @return: An integer
     */
    public int pop() {
        while (s1.size() > 1) {
            s2.push(s1.pop());
        }
        int popVal = s1.pop();
        move();
        return popVal;
    }

    /*
     * @return: An integer
     */
    public int top() {
        while (s1.size() > 1) {
            s2.push(s1.pop());
        }
        int topVal = s1.peek();
        move();
        return topVal;
    }

    private void move() {
        while (s2.size() > 0) {
            s1.push(s2.pop());
        }
    }
}
```

## Solution 2 \(Java\)

```java
public class MyQueue {

    Deque<Integer> s1 = new ArrayDeque<>();
    Deque<Integer> s2 = new ArrayDeque<>();

    public MyQueue() {

    }

    /*
     * @param element: An integer
     * @return: nothing
     */
    public void push(int element) {
        s1.push(element);
    }

    /*
     * @return: An integer
     */
    public int pop() {
        if (s2.isEmpty())
            move();
        return s2.pop();
    }

    /*
     * @return: An integer
     */
    public int top() {
        if (s2.isEmpty())
            move();
        return s2.peek();
    }

    private void move() {
        while (!s1.isEmpty()) {
            s2.push(s1.pop());
        }
    }
}

// s1 = []
// s2 = [3,2,1]
```

