---
description: ID: 494; easy
---
# Implement Stack by Two Queues

{% embed url="https://www.lintcode.com/problem/494/" %}

{% embed url="https://leetcode.com/problems/implement-stack-using-queues/" %}

## Solution 1 (Java)

```java
public class Stack {

    private Queue<Integer> q1 = new ArrayDeque<>();
    private Queue<Integer> q2 = new ArrayDeque<>();

    /*
     * @param x: An integer
     * @return: nothing
     */
    public void push(int x) {
        q1.offer(x);
    }

    /*
     * @return: nothing
     */
    public void pop() {
        if (q2.isEmpty())
            move();
        q1.poll();
        swap();
    }

    /*
     * @return: An integer
     */
    public int top() {
        if (q2.isEmpty())
            move();
        int topVal = q1.poll();
        q2.offer(topVal);
        swap();
        return topVal;
    }

    /*
     * @return: True if the stack is empty
     */
    public boolean isEmpty() {
        return q1.isEmpty() && q2.isEmpty();
    }

    private void move() {
        while (q1.size() > 1) {
            q2.offer(q1.poll());
        }
    }

    private void swap() {
        Queue<Integer> temp = q1;
        q1 = q2;
        q2 = temp;
    }
}

// push(1), push(2), push(3), pop, push(4), top()
// q1 = []
// q2 = [1,2,4]
```

### Notes

* LintCode

## Solution 2 (Java)

```java
class MyStack {
    
    Queue<Integer> q1;
    Queue<Integer> q2;

    /** Initialize your data structure here. */
    public MyStack() {
        q1 = new ArrayDeque<>();
        q2 = new ArrayDeque<>();
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        q1.offer(x);
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        while (q1.size() > 1) {
            q2.offer(q1.poll());
        }
        int popVal = q1.poll();
        moveBack();
        return popVal;
    }
    
    /** Get the top element. */
    public int top() {
        while (q1.size() > 1) {
            q2.offer(q1.poll());
        }
        int topVal = q1.peek();
        q2.offer(q1.poll());
        moveBack();
        return topVal;
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return q1.isEmpty();
    }
    
    private void moveBack() {
        while (!q2.isEmpty()) {
            q1.offer(q2.poll());
        }
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```

### Notes

* LeetCode
