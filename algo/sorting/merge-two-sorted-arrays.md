---
description: ID: 6; easy
---
# Merge Two Sorted Arrays

{% embed url="https://www.lintcode.com/problem/6/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param A: sorted integer array A
     * @param B: sorted integer array B
     * @return: A new sorted integer array
     */
    public int[] mergeSortedArray(int[] A, int[] B) {
        if (A == null) return B;
        if (B == null) return A;

        int[] ans = new int[A.length + B.length];
        int i = 0, j = 0, k = 0;
        while (i < A.length && j < B.length) {
            ans[k++] = A[i] < B[j] ? A[i++] : B[j++];
        }
        while (i < A.length) {
            ans[k++] = A[i++];
        }
        while (j < B.length) {
            ans[k++] = B[j++];
        }

        return ans;
    }
}
```

## Solution 2 (Java)

```java
public class Solution {
    /**
     * @param A: sorted integer array A
     * @param B: sorted integer array B
     * @return: A new sorted integer array
     */
    public int[] mergeSortedArray(int[] A, int[] B) {
        if (A == null || A.length == 0) return B;
        if (B == null || B.length == 0) return A;
        
        int lenA = A.length;
        int lenB = B.length;
        
        int[] res = new int[lenA + lenB];
        int i = 0, j = 0;
        for (int k = 0; k < lenA + lenB; k++) {
            if (i < lenA && (j >= lenB || A[i] <= B[j])) {
                res[k] = A[i++];
            } else {
                res[k] = B[j++];
            }
        }
        
        return res;
    }
}
```

## Solution 3 (Java)

```java
public class Solution {
    /**
     * @param A: sorted integer array A
     * @param B: sorted integer array B
     * @return: A new sorted integer array
     */
    public int[] mergeSortedArray(int[] A, int[] B) {
        if (A == null) return B;
        if (B == null) return A;

        int[] res = new int[A.length + B.length];
        int i = 0, k = 0;
        for (int j = 0; j < B.length; j++) {
            int pos = binarySearch(A, B[j]);
            while (i < pos) {
                res[k++] = A[i++];
            }
            res[k++] = B[j];
        }
        while (i < A.length) {
            res[k++] = A[i++];
        }
        return res;
    }

    private int binarySearch(int[] A, int target) {
        int left = 0;
        int right = A.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if(A[mid] == target) {
                return mid;
            } else if(target < A[mid]){
                right = mid - 1;
            } else{
                left = mid + 1;
            }
        }
        return left;
    }
}
```

### Notes

* This solution is to handle the challenge: How can you optimize your algorithm if one array is very large and the other is very small?\
