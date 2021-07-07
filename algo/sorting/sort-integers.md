---
description: 'ID: 463; naive'
---

# Sort Integers

{% embed url="https://www.lintcode.com/problem/463/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param A: an integer array
     * @return: nothing
     */
    public void sortIntegers(int[] A) {
        for (int i = 0; i < A.length; i++) {
            int minIndex = i;
            for (int j = i; j < A.length; j++) {
                if (A[j] < A[minIndex]) {
                    minIndex = j;
                }
            }
            int temp = A[i];
            A[i] = A[minIndex];
            A[minIndex] = temp;
        }
    }
}
```

### Notes

* **Selection sort**
* Each time, find the minimum number and swap it with the first number of the unsorted list.

## Solution 2 \(Java\)

```java
public class Solution {
    /**
     * @param A: an integer array
     * @return: nothing
     */
    public void sortIntegers(int[] A) {
        for (int i = 0; i < A.length; i++) {
            int num = A[i];
            int j = i - 1;
            while (j >= 0 && A[j] > num) {
                A[j + 1] = A[j];
                j--;
            }
            A[j + 1] = num;
        }
    }
}
```

### Notes

* **Insertion sort**
* This is similar to playing card and sorting them. If the current number is larger than its previous number, we make space and move it to a proper position to the left.

## Solution 3 \(Java\)

```java
public class Solution {
    /**
     * @param A: an integer array
     * @return: nothing
     */
    public void sortIntegers(int[] A) {
        while (true) {
            boolean swap = false;
            for (int i = 0; i < A.length - 1; i++) {
                if (A[i] > A[i + 1]) {
                    int temp = A[i];
                    A[i] = A[i + 1];
                    A[i + 1] = temp;
                    swap = true;
                }
            }
            if (!swap) break;
        }
    }
}
```

### Notes

* Bubble sort
* We look at the numbers in pairs. If there is an inversion in the pair, we swap the two numbers. We keep swapping until we cannot swap.

