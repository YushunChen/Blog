---
description: 'ID: 75; medium; 寻找峰值'
---

# Find Peak Element

{% embed url="https://www.lintcode.com/problem/75/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param A: An integers array.
     * @return: return any of peek positions.
     */
    public int findPeak(int[] A) {
        int left = 0, right = A.length - 1;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (A[mid] > A[mid-1] && A[mid] > A[mid+1]) {
                return mid;
            } else if (A[mid] > A[mid-1] && A[mid] < A[mid+1]) {
                left = mid;
            } else {
                right = mid;
            }
        }
        return A[left] > A[right] ? left : right;
    }
}
```

