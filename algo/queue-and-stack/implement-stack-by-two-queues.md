---
description: 'ID: 494; easy'
---

# Implement Stack by Two Queues

{% embed url="https://www.lintcode.com/problem/494/" %}

## Solution 1 \(Java\)

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

