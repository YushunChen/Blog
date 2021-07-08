---
description: 'ID: 846; easy'
---

# Multi-keyword Sort

{% embed url="https://www.lintcode.com/problem/846/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param array: the input array
     * @return: the sorted array
     */
    public int[][] multiSort(int[][] array) {
        for (int i = 0; i < array.length; i++) {
            for (int j = i + 1; j < array.length; j++) {
                if (compare(array[i], array[j])) {
                    int[] temp = array[i];
                    array[i] = array[j];
                    array[j] = temp;
                }
            }
        }
        return array;
    }

    private boolean compare(int[] a, int[] b) {
        if (a[1] == b[1]) {
            return a[0] > b[0];
        }
        return a[1] < b[1];
    }
}
```

