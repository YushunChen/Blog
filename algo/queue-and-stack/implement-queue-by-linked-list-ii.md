---
description: ID: 493; easy
---
# Implement Queue by Linked List II

{% embed url="https://www.lintcode.com/problem/493/" %}

## Solution 1 (Java)

```java
class Node {
    public int val;
    public Node prev, next;
    public Node(int val) {
        this.val = val;
        prev = next = null;
    }
}

public class Dequeue {

    private Node head, tail;

    public Dequeue() {
        head = tail = null;
    }

    /*
     * @param item: An integer
     * @return: nothing
     */
    public void push_front(int item) {
        if (head == null) {
            head = new Node(item);
            tail = head;
        } else {
            Node newNode = new Node(item);
            head.prev = newNode;
            newNode.next = head;
            head = newNode;
        }
    }

    /*
     * @param item: An integer
     * @return: nothing
     */
    public void push_back(int item) {
        if (tail == null) {
            tail = new Node(item);
            head = tail;
        } else {
            Node newNode = new Node(item);
            newNode.prev = tail;
            tail.next = newNode;
            tail = newNode;
        }
    }

    /*
     * @return: An integer
     */
    public int pop_front() {
        if (head != null) {
            int item = head.val;
            head = head.next;
            if (head != null) {
                head.prev = null;
            } else {
                tail = null;
            }
            return item;
        }
        return -1;
    }

    /*
     * @return: An integer
     */
    public int pop_back() {
        if (tail != null) {
            int item = tail.val;
            tail = tail.prev;
            if (tail != null) {
                tail.next = null;
            } else {
                head = null;
            }
            return item;
        }
        return -1;
    }
}
```
