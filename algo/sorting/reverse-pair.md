---
description: 'ID: 532; medium'
---

# Reverse Pair

{% embed url="https://www.lintcode.com/problem/532/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param A: an array
     * @return: total of reverse pairs
     */
    public long reversePairs(int[] A) {
        if (A == null || A.length == 0)
            return 0;
        int[] temp = new int[A.length];
        return reversePairsHelper(A, 0, A.length - 1, temp);
    }

    private int reversePairsHelper(int[] A, int left, int right, int[] temp) {
        if (left >= right) return 0;
        int mid = left + (right - left) / 2;
        int res = 0;

        res += reversePairsHelper(A, left, mid, temp);
        res += reversePairsHelper(A, mid + 1, right, temp);

        int i = left, j = mid + 1;
        for (int k = 0; k < right - left + 1; k++) {
            if (i <= mid && (j > right || A[i] <= A[j])) {
                temp[k] = A[i++];
            } else {
                temp[k] = A[j++];
                if (i <= mid) {
                    res += mid - i + 1;
                }
            }
        }
        for (int k = 0; k < right - left + 1; k++) {
            A[left + k] = temp[k];
        }
        return res;
    }
}
```

### Notes

* We use **merge sort** in this solution, sorting while counting the inversions.

