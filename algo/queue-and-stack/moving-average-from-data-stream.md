---
description: 'ID: 642; easy'
---

# Moving Average from Data Stream

{% embed url="https://www.lintcode.com/problem/642/" %}

## Solution 1 \(Java\)

```java
public class MovingAverage {

    Queue<Integer> q;
    double sum;
    int size;

    /*
    * @param size: An integer
    */
    public MovingAverage(int size) {
        q = new ArrayDeque<>();
        sum = 0;
        this.size = size;
    }

    /*
     * @param val: An integer
     * @return:  
     */
    public double next(int val) {
        sum += val;
        if (q.size() == size) {
            int pollVal = q.poll();
            sum -= pollVal;
        }
        q.offer(val);
        return sum / q.size();
    }
}
```

