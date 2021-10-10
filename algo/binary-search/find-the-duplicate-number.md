---
description: ID: 633; medium; 寻找重复的数
---
# Find the Duplicate Number

{% embed url="https://www.lintcode.com/problem/633/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param nums: an array containing n + 1 integers which is between 1 and n
     * @return: the duplicate one
     */
    public int findDuplicate(int[] nums) {
        int left = 1, right = nums.length;

        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (countSmallerNums(mid, nums) <= mid) {
                left = mid;
            } else {
                right = mid;
            }
        }

        if (countSmallerNums(left, nums) <= left)
            return right;
        return left;
    }

    private int countSmallerNums(int num, int[] nums) {
        int count = 0;
        for (int n : nums) {
            if (n <= num) count++;
        }
        return count;
    }
}
```

### Notes

* The array is not sorted
* Time complexity should be less than

$$
O(n^2)
$$

* Space complexity should be

$$
O(1)
$$

We know that the range of the numbers is initially `[1, n]`. We take the middle element inside the range `mid`. If `count ≤ mid`, where `count` is the number of elements that are less than or equal to `mid`, then we are certain that the duplicated number is not inside the range `[left, mid]`. The reason is the following:

{% tabs %}
{% tab title="Example 1" %}
Original array: `[3, 1, 4, 6, 5, 8, 8, 9]` 

Range: `[1, 9]`

| left | right | mid | count                                   | Result        |
| ---- | ----- | --- | --------------------------------------- | ------------- |
| 1    | 9     | 5   | 4 bc the smaller number are  3, 1, 4, 5 | `count ≤ mid` |

New range is `[5, 9]` and 8 is inside that range.:white_check_mark: 
{% endtab %}

{% tab title="Example 2" %}
Original array: `[3, 1, 1, 1, 4, 6, 5, 8]` 

Range: `[1, 8]`

| left | right | mid | count                                      | Result        |
| ---- | ----- | --- | ------------------------------------------ | ------------- |
| 1    | 8     | 4   | 5 bc the smaller number are  3, 1, 1, 1, 4 | `count > mid` |

New array is `[1, 4]` and 1 is inside that range.:white_check_mark: 
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Maybe think about `[3, 8, 8, 4, 6, 1, 5, 9]`. Length - 1?
{% endhint %}



* Time complexity for this solution is

$$
O(n\log{n})
$$

* Space complexity should be

$$
O(1)
$$
