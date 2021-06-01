---
description: 'ID: 447; medium; 在大数组中查找'
---

# Search in a Big Sorted Array

{% embed url="https://www.lintcode.com/problem/447/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param reader: An instance of ArrayReader.
     * @param target: An integer
     * @return: An integer which is the first index of target.
     */
    public int searchBigSortedArray(ArrayReader reader, int target) {
        int left = 0, right = 1;
        while (reader.get(right) < target) {
            right *= 2;
        }

        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            int midNum = reader.get(mid);
            if (midNum < target) {
                left = mid;
            } else {
                right = mid;
            }
        }

        if (reader.get(left) == target) return left;
        if (reader.get(right) == target) return right;
        return -1;
    }
}
```

### Ideas

* We do not know the upper bound of the range, so we double `right` starting from 1 until the element at right is larger than the `target`. Thus, we have a valid range containing a `target`.
* We cannot return `mid` immediately if we found a `target` because the problem requires the first position of the `target`.

