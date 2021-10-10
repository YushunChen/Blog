---
description: ID: 546; easy
---
# Implement Queue by Interface

{% embed url="https://www.lintcode.com/problem/546/" %}

## Solution 1 (Java)

```java
interface InterfaceQueue {
    void push(int element);

    // define an interface for pop method
    /* write your code here */
    int pop();

    // define an interface for top method
    /* write your code here */
    int top();
}

class Node {
    public int val;
    public Node prev, next;
    public Node(int val) {
        this.val = val;
        prev = next = null;
    }
}

public class MyQueue implements InterfaceQueue {
    /* you can declare your private attributes here */
    private Node first, last;
    public MyQueue() {
       first = last = null;
    }

    // implement the push method
    /* write your code here */
    @Override
    public void push(int val) {
       if (last == null) {
           last = new Node(val);
           first = last;
       } else {
           Node newNode = new Node(val);
           last.next = newNode;
           newNode.prev = last;
           last = newNode;
       }
    }
	
    // implement the pop method
    /* write your code here */
    @Override
    public int pop() {
        if (first == null)
            return -1;
        int popVal = first.val;
        first = first.next;
        if (first == null) {
            last = null;
        } else {
            first.prev = null;
        }
        return popVal;
    }
    
	// implement the top method
    /* write your code here */
    @Override
    public int top() {
        if (first == null)
            return -1;
        return first.val;
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue queue = new MyQueue();
 * queue.push(123);
 * queue.top(); will return 123;
 * queue.pop(); will return 123 and pop the first element in the queue
 */
```
