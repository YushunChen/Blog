---
description: 'ID: 62; medium; 搜索旋转排序数组'
---

# Search in Rotated Sorted Array

{% embed url="https://www.lintcode.com/problem/62/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param A: an integer rotated sorted array
     * @param target: an integer to be searched
     * @return: an integer
     */
    public int search(int[] A, int target) {
        if (A == null || A.length == 0) return -1;
        int left = 0, right = A.length - 1;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (A[mid] == target) return mid;

            // mid element on the left half
            if (A[mid] > A[left]) {
                if (target >= A[left] && target < A[mid]) {
                    right = mid;
                } else {
                    left = mid;
                }
            } else {
                // mid element on the right half
                if (target > A[mid] && target <= A[right]) {
                    left = mid;
                } else {
                    right = mid;
                }
            }
        }
        if (A[left] == target) return left;
        if (A[right] == target) return right;
        return -1;
    }
}
```

### Notes

In order to perform a classical binary search, we need to have a strictly increasing or decreasing series. Here, the rotate array can be seen as two increasing arrays. We need to determine which half we should perform the operations on. Thus, we compare the `mid` element with the first element in the array to see which half the `mid` element is on currently.

#### I. The `mid` element is on the left half

The reason is that if the `mid` element is larger than the first element, by the construction of the rotated array, we know that the `mid` element is on the left half now. After this first check, we try to see where `target` is. We compare if the `target` is on the same half \(left half\) as the mid element. This comparison is simple checking if `target` is in between `A[left]` and `A[mid]`.

1. If `target` and the `mid` element are on the same half \(`target` is on the left half\), we can discard the right half of the array.
2. If they are on different halves \(`target` is on the right half\), we can discard the left half.

#### II. The `mid` element is on the right half

If the `mid` element is smaller than the first element, then it is on the right half. Similarly, we try to see where `target` is. If `target` is in between `A[mid]` and `A[right]`, then `target` is on the same half as the `mid` element \(right half\). 

1. If `target` and the `mid` element are on the same half \(`target` is on the right half\), we can discard the left half of the array.
2. If they are on different halves \(`target` is on the left half\), we can discard the right half.

### Example

{% tabs %}
{% tab title="Example 1" %}
`[4, 5, 6, 7, 0, 1, 2]` and `target = 5`

| left | right | mid | New Range |
| :--- | :--- | :--- | :--- |
| 4 | 2 | 7 | `[4, 5, 6, 7]` |
| 4 | 7 | 5 | `[4, 5]` |

Case I. 1.: The `mid` element and `target` are both on the left side. Loop terminates, the index of 5 is returned.
{% endtab %}

{% tab title="Example 2" %}
`[4, 5, 6, 7, 0, 1, 2]` and `target = 2`

| left | right | mid | New Range |
| :--- | :--- | :--- | :--- |
| 4 | 2 | 7 | `[7, 0, 1, 2]` |
| 7 | 2 | 0 | `[0, 1, 2]` |
| 0 | 2 | 1 | `[1, 2]` |

Case I. 2. and Case II. 1.: To start with, the `mid` element and `target` are on different sides \(`mid` is on the left, `target` is on the right\). Then, after iteration 1, the `mid` element and `target` are on the same side. 

Loop terminates, the index of 2 is returned.
{% endtab %}

{% tab title="Example 3" %}
`[6, 7, 0, 1, 2, 3, 4, 5]` and `target = 6`

| left | right | mid | New Range |
| :--- | :--- | :--- | :--- |
| 6 | 5 | 1 | `[6, 7, 0, 1]` |
| 6 | 1 | 7 | `[6, 7]` |

Case II. 2. and Case I. 1.: To start with, the `mid` element and `target` are on different sides \(`mid` is on the right, `target` is on the left\). Then, after iteration 1, the `mid` element and `target` are on the same side. 

Loop terminates, the index of 6 is returned.
{% endtab %}

{% tab title="Example 4" %}
`[0, 1, 2, 3, 4, 5]` and `target = 4`

| left | right | mid | New Range |
| :--- | :--- | :--- | :--- |
| 0 | 5 | 2 | `[2, 3, 4, 5]` |
| 2 | 5 | 3 | `[3, 4, 5]` |
| 3 | 5 | 4 | 4 immediately returned |

The algorithm works for non-rotated arrays as well. This can also be seen in previous examples.

Loop terminates, the index of 4 is returned.
{% endtab %}
{% endtabs %}

