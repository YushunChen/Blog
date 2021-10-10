---
description: ID: 61; medium; 搜索区间
---
# Search for a Range

{% embed url="https://www.lintcode.com/problem/61/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param A: an integer sorted array
     * @param target: an integer to be inserted
     * @return: a list of length 2, [index1, index2]
     */
    public int[] searchRange(int[] A, int target) {
        if (A == null || A.length == 0) {
            return new int[]{-1, -1};
        }

        int[] range = new int[2];
        int left = 0, right = A.length - 1;

        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (A[mid] < target) {
                left = mid;
            } else {
                right = mid;
            }
        }
        if (A[left] == target) {
            range[0] = left;
        } else if (A[right] == target) {
            range[0] = right;
        } else {
            range[0] = range[1] = -1;
            return range;
        }

        left = 0; right = A.length - 1;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (A[mid] > target) {
                right = mid;
            } else {
                left = mid;
            }
        }
        if (A[right] == target) {
            range[1] = right;
        } else if (A[left] == target) {
            range[1] = left;
        } else {
            range[0] = range[1] = -1;
            return range;
        }

        return range;
    }
}
```

{% hint style="info" %}
Similar to Total Occurrence of Target (ID: 462).
{% endhint %}
