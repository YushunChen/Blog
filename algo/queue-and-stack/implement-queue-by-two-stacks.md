---
description: 'ID: 40; medium'
---

# Implement Queue by Two Stacks

{% embed url="https://www.lintcode.com/problem/40/" %}

{% embed url="https://leetcode.com/problems/implement-queue-using-stacks/" %}

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

## Solution 3 \(Java\)

```java
class MyQueue {

    Deque<Integer> s1;
    Deque<Integer> s2;
    
    /** Initialize your data structure here. */
    public MyQueue() {
        s1 = new ArrayDeque<>();
        s2 = new ArrayDeque<>();
    }
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        s1.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        move();
        int pollVal = s1.pop();
        moveBack();
        return pollVal;
    }
    
    /** Get the front element. */
    public int peek() {
        move();
        int peekVal = s1.peek();
        s2.push(s1.pop());
        moveBack();
        return peekVal;
        
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return s1.isEmpty();
    }
    
    private void move() {
        while (s1.size() > 1) {
            s2.push(s1.pop());
        }
    }
    private void moveBack() {
        while (!s2.isEmpty()) {
            s1.push(s2.pop());
        }
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```

### Notes

* Same method for LeetCode.

