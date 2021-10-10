---
description: ID; 183; hard; 木材加工
---
# Wood Cut

{% embed url="https://www.lintcode.com/problem/183/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param L: Given n pieces of wood with length L[i]
     * @param k: An integer
     * @return: The maximum length of the small pieces
     */
    public int woodCut(int[] L, int k) {
        if (L == null || L.length == 0) 
            return 0;
        int maxLength = findMaxWoodLength(L);
        int left = 1, right = maxLength;

        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            int counts = countPieces(L, mid);
            if (counts >= k) {
                left = mid;
            } else {
                right = mid;
            }
        }

        if (countPieces(L, right) >= k) return right;
        if (countPieces(L, left) >= k) return left;
        return 0;
    }

    private int findMaxWoodLength(int[] L) {
        int max = 0;
        for (int l : L) {
            max = Math.max(max, l);
        }
        return max;
    }

    private int countPieces(int[] L, int cutLength) {
        int counts = 0;
        for (int l : L) {
            counts += l / cutLength;
        }
        return counts;
    }
}
```

### Notes

There are two key requirements in this problem:

1. The woods need to be cut into `k` pieces of the same length.
2. The length of the pieces should be maximized.

We use binary search to search for the cut length, i.e., the length of the pieces. The initial range for this length is `[1, max]` where `max` is the maximum length among the woods. We take the middle number and count the number of pieces using that number as the cut length. 

* If `count ≥ k`, the first requirement is satisfied but we still need to test the second requirement, so we do not immediately return. Now the new range is `[mid, max]`.
* If `count < k`, the first requirement is not satisfied, which means we are cutting too much. Then, the new range is `[1, mid]`.

Lastly, we end up with the range `[left, right]`. To satisfy the two requirements, we would return `right` if possible since `right` is larger than `left`.
