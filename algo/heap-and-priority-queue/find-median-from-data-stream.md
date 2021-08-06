---
description: 'ID: 81; hard'
---

# Find Median from Data Stream

{% embed url="https://www.lintcode.com/problem/81/" %}

## Solution 1 \(Java\)

```java
public class Solution {

    PriorityQueue<Integer> minHeap, maxHeap;
    int median;
    boolean isFirstNum;
    public Solution() {
        minHeap = new PriorityQueue<>();
        maxHeap = new PriorityQueue<>(new Comparator<Integer>() {
            public int compare(Integer x, Integer y) {
                return y - x;
            }
        });
        isFirstNum = true;
    }

    /**
     * @param val: An integer
     * @return: nothing
     */
    public void add(int val) {
        if (isFirstNum) {
            median = val;
            isFirstNum = false;
            return;
        }

        if (val < median) {
            maxHeap.offer(val);
        } else {
            minHeap.offer(val);
        }

        if (maxHeap.size() > minHeap.size()) {
            minHeap.offer(median);
            median = maxHeap.poll();
        }
        if (maxHeap.size() < minHeap.size() - 1) {
            maxHeap.offer(median);
            median = minHeap.poll();
        }
    }

    /**
     * @return: return the median of the data stream
     */
    public int getMedian() {
        return median;
    }
}
```

### Notes

* We used a `maxHeap` and a `minHeap` to maintain the data stream. The `maxHeap` stores numbers that are less than the `median`. The `minHeap` stores numbers that are larger than the `median`. Then, we update the median whenever the two heaps have sizes that differ by 2 \(to be more precise, see the condition in code\). By construction, the results by polling either the `minHeap` or the `maxHeap` will be the current `median`. Eventually, we just return the current `median`.

