---
description: 'ID: 360; hard'
---

# Sliding Window Median

{% embed url="https://www.lintcode.com/problem/360/" %}

## Solution 1 \(Java\)

```java
public class Solution {

    private PriorityQueue<Integer> minHeap, maxHeap;

    /**
     * @param nums: A list of integers
     * @param k: An integer
     * @return: The median of the element inside the window at each moving
     */
    public List<Integer> medianSlidingWindow(int[] nums, int k) {
        List<Integer> res = new ArrayList<>();
        if (nums == null || nums.length == 0) 
            return res;
        int n = nums.length;
        minHeap = new PriorityQueue<>(n);
        maxHeap = new PriorityQueue<>(n, Collections.reverseOrder());

        for (int i = 0; i < n; i++) {
            if (maxHeap.isEmpty() || nums[i] <= maxHeap.peek()) {
                maxHeap.offer(nums[i]);
            } else {
                minHeap.offer(nums[i]);
            }

            balance();
            if (i - k >= 0) {
                if (nums[i - k] > maxHeap.peek()) {
                    minHeap.remove(nums[i - k]);
                } else {
                    maxHeap.remove(nums[i - k]);
                }
            }

            balance();
            if (i >= k - 1) {
                res.add(maxHeap.peek());
            }
        }
        return res;
    }

    private void balance() {
        while (maxHeap.size() < minHeap.size()) {
            maxHeap.offer(minHeap.poll());
        }
        while (minHeap.size() < maxHeap.size() - 1) {
            minHeap.offer(maxHeap.poll());
        }
    }
}
```

### Notes

* Similar to [Find Median from Data Stream](find-median-from-data-stream.md), we used a minHeap and a maxHeap to maintain the window.
* One more operation needed is to remove the previous number that is outside the current window.

