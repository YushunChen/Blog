---
description: ID: 545; medium
---
# Top k Largest Numbers II

{% embed url="https://www.lintcode.com/problem/545/" %}

## Solution 1 (Java)

```java
public class Solution {

    private Queue<Integer> minheap;
    private int capacity;

    /*
    * @param k: An integer
    */
    public Solution(int k) {
        minheap = new PriorityQueue<>();
        capacity = k;
    }

    /*
     * @param num: Number to be added
     * @return: nothing
     */
    public void add(int num) {
        if (minheap.size() < capacity) {
            minheap.offer(num);
            return;
        } 
        if (num > minheap.peek()) {
            minheap.poll();
            minheap.offer(num);
        }
    }

    /*
     * @return: Top k element
     */
    public List<Integer> topk() {
        // convert heap to list by initialization
        List<Integer> res = new ArrayList<>(minheap);
        Collections.sort(res, Collections.reverseOrder());
        return res;

        // // Use iterator
        // List<Integer> res = new ArrayList<>();
        // Iterator it = minheap.iterator();
        // while (it.hasNext()) {
        //     res.add((Integer)it.next());
        // }
        // Collections.sort(res, Collections.reverseOrder());
        // return res;
    }
}
```

### Notes

* It is important to notice here that we used a min heap. Otherwise, we do not know when to offer or poll based on the number and also the size of the heap.
* Do not forget to reverse the order since the problem is asking for the top k largest numbers.

## Solution 2 (Java)

```java
public class Solution {

    private int[] heap;
    private int n;
    private int maxSize;
    /*
    * @param k: An integer
    */
    public Solution(int k) {
        heap = new int[k];
        maxSize = k;
    }

    /*
     * @param num: Number to be added
     * @return: nothing
     */
    public void add(int num) {
        if (n < maxSize) {
            offer(num);
        } else {
            if (num > heap[0]) {
                poll();
                offer(num);
            }
        }
    }

    /*
     * @return: Top k element
     */
    public List<Integer> topk() {
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            res.add(heap[i]);
        }
        Collections.sort(res, Collections.reverseOrder());
        return res;
    }

    /*
     * add the number to the last element in the heap and then sift up
     */
    private void offer(int num) {
        heap[n] = num;
        int k = n;
        n++;

        // sift up
        while (k > 0) {
            int parent = (k - 1) / 2;
            if (heap[k] > heap[parent])
                break;
            int temp = heap[k];
            heap[k] = heap[parent];
            heap[parent] = temp;
            k = parent;
        }
    }

    /*
     * swap the top number with the last element and sift down the last element
     */
    private void poll() {
        heap[0] = heap[n - 1];
        int k = 0;
        n--;

        // sift down
        while (true) {
            int left = k * 2 + 1;
            int right = left + 1;
            int minIndex = k;
            if (left < n && heap[left] < heap[minIndex]) {
                minIndex = left;
            }
            if (right < n && heap[right] < heap[minIndex]) {
                minIndex = right;
            }
            if (minIndex == k) break;
            int temp = heap[minIndex];
            heap[minIndex] = heap[k];
            heap[k] = temp;
            k = minIndex;
        }
    }
}
```

### Notes

* This is a version of the solution if we do not use a built-in priority queue.
* This solution utilizes the sift up and sift down methods used in [Heapify](heapify.md).
