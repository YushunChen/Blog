---
description: ID: 495; easy
---
# Implement Stack

{% embed url="https://www.lintcode.com/problem/495/" %}

## Solution 1 (Java)

```java
public class Stack {

    private List<Integer> arr = new ArrayList<>();

    /*
     * @param x: An integer
     * @return: nothing
     */
    public void push(int x) {
        arr.add(x);
    }

    /*
     * @return: nothing
     */
    public void pop() {
        if (isEmpty())
            return;
        arr.remove(arr.size() - 1);
    }

    /*
     * @return: An integer
     */
    public int top() {
        if (isEmpty())
            return -1;
        return arr.get(arr.size() - 1);
    }

    /*
     * @return: True if the stack is empty
     */
    public boolean isEmpty() {
        if (arr == null || arr.size() == 0)
            return true;
        return false;
    }
}
```
