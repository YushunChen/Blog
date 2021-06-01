---
description: 'ID: 462; easy; 目标出现总和'
---

# Total Occurrence of Target

{% embed url="https://www.lintcode.com/problem/462/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param A: A an integer array sorted in ascending order
     * @param target: An integer
     * @return: An integer
     */
    public int totalOccurrence(int[] A, int target) {
        if (A == null || A.length == 0) {
            return 0;
        }

        int start, end;
        int left = 0, right = A.length - 1;

        // find left end point of the range
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (A[mid] < target) {
                left = mid;
            } else {
                right = mid;
            }
        }
        if (A[left] == target) {
            start = left;
        } else if (A[right] == target) {
            start = right;
        } else {
            return 0;
        }

        // find right end point of the range
        left = 0; right = A.length -1;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (A[mid] > target) {
                right = mid;
            } else {
                left = mid;
            }
        }
        if (A[right] == target) {
            end = right;
        } else if (A[left] == target) {
            end = left;
        } else {
            return 0;
        }

        return end - start + 1;
    }
}
```

