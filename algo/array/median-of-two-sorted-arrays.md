---
description: 'ID: 4; hard'
---

# Median of Two Sorted Arrays

{% embed url="https://leetcode.com/problems/median-of-two-sorted-arrays" %}

## Solution 1 (Java)

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int N = nums1.length + nums2.length;
        if (N % 2 == 0) {
            return (findKthNumber(nums1, 0, nums2, 0, N / 2) 
                    + findKthNumber(nums1, 0, nums2, 0, N / 2 + 1)) / 2;
        }
        return findKthNumber(nums1, 0, nums2, 0, N / 2 + 1);
    }

    private double findKthNumber(int[] A, int startOfA, int[] B, int startOfB, int k) {
        if (startOfA >= A.length) {
            return B[startOfB + k - 1];
        }
        if (startOfB >= B.length) {
            return A[startOfA + k - 1];
        }
        if (k == 1) {
            return Math.min(A[startOfA], B[startOfB]);
        }
        
        int halfKthOfA = startOfA + k / 2 - 1 >= A.length ? Integer.MAX_VALUE : A[startOfA + k / 2 - 1];
        int halfKthOfB = startOfB + k / 2 - 1 >= B.length ? Integer.MAX_VALUE : B[startOfB + k / 2 - 1];
        if (halfKthOfA < halfKthOfB) {
            return findKthNumber(A, startOfA + k / 2, B, startOfB, k - k / 2);
        } else {
            return findKthNumber(A, startOfA, B, startOfB + k / 2, k - k / 2);
        }

    }

}
```

### Notes

* We use divide and conquer in this problem. We change the problem to find the k-th number of two sorted arrays, where k represents the index of the median.
* Inside the helper method,
  * If either A or B runs out of elements first, then we just use the current k-th element of the other array.
  * If k == 1, which means we need the first number, then we pick the smaller one from A or B.
  * Then we count half of k steps for both A and B. We shrink the range based on which one is smaller. Note we only update the index for the array with the smaller element and also do not forget to update k.
