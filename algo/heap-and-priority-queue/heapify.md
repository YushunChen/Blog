---
description: ID: 130; medium
---
# Heapify

{% embed url="https://www.lintcode.com/problem/130/" %}

## Solution 1 (Java)

```java
public class Solution {
    /*
     * @param A: Given an integer array
     * @return: nothing
     */
    public void heapify(int[] A) {
        for (int i = 0; i < A.length; i++) {
            siftUp(A, i);
        }
    }

    private void siftUp(int[] A, int k) {
        while (k != 0) {
            int pIndex = (k - 1) / 2;
            if (A[k] > A[pIndex])
                break;

            int temp = A[k];
            A[k] = A[pIndex];
            A[pIndex] = temp;

            k = pIndex;
        }
    }
}
```

### Notes

* This is the `siftUp` version of the problem. If we are sifting the node up, we should make sure it is smaller than its parent. If it is already larger than its parent, we do nothing.
* Time complexity: `O(nlogn)`

## Solution 2 (Java)

```java
public class Solution {
    /*
     * @param A: Given an integer array
     * @return: nothing
     */
    public void heapify(int[] A) {
        for (int i = A.length / 2; i >= 0; i--) {
            siftDown(A, i);
        }
    }

    private void siftDown(int[] A, int k) {
        while (k < A.length) {
            int left = 2 * k + 1;
            int right = left + 1;
            int minIndex = k;
            if (left < A.length && A[left] < A[minIndex])
                minIndex = left;
            if (right < A.length && A[right] < A[minIndex])
                minIndex = right;
            if (minIndex == k)
                break;
            
            int temp = A[minIndex];
            A[minIndex] = A[k];
            A[k] = temp;

            k = minIndex;
        }
    }
}
```

```java
        1
      /   \
     2     3
    / \
   4   5

// [1, 2, 3, 4, 5]
// i = 0, k = 2
// minIndex = 2, left = 1, right = 2
```

### Notes

* This is the `siftDown` version of the problem. If we are sifting down the node, we should make sure that the node is smaller than its left and right children. Then, we swap the node with the smaller one of the two children. 
* Time complexity: `O(n)`. This time complexity is important to understand. The reason is that we start sifting down at the n / 2 position. So approximately, n / 4 numbers are swapped 1 time; n / 8 numbers are swapped 2 times; n / 16 numbers are swapped 3 times, etc. So the time complexity is:

$$
O(\frac{n}{4}\times1+\frac{n}{8}\times2+\frac{n}{16}\times3+\cdots+1\times \log(n)) = O(n)
$$

* The calculation can be down in the following way:

$$
s = \frac{n}{4}\times1+\frac{n}{8}\times2+\frac{n}{16}\times3+\cdots
$$

$$
2s = \frac{n}{2}\times1+\frac{n}{4}\times2+\frac{n}{8}\times3+\cdots
$$

$$
s = 2s - s = \frac{n}{2}+\frac{n}{4}+\frac{n}{8}+\frac{n}{16}\cdots=n
$$
