---
description: ID: 610; medium
---
# Two Sum - Difference equals to target

{% embed url="https://www.lintcode.com/problem/610/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param nums: an array of Integer
     * @param target: an integer
     * @return: [num1, num2] (num1 < num2)
     */
    public int[] twoSum7(int[] nums, int target) {
        int[] res = new int[2];
        target = Math.abs(target);
        for (int i = 0, j = 1; j < nums.length; j++) {
            while (i < j && nums[j] - nums[i] > target) {
                i++;
            }
            if (i != j && nums[j] - nums[i] == target) {
                res[0] = nums[i];
                res[1] = nums[j];
                if (res[0] > res[1]) {
                    int temp = res[0];
                    res[0] = res[1];
                    res[1] = temp;
                }
                return res;
            }
        }
        return res;
    }
}
```

### Notes

* Two pointers `i` and `j`
* We move the `i` pointer in this solution to narrow down the range of the two numbers.
* Time complexity: `O(n)`
* Space complexity: `O(1)`

## Solution 2 (Java)

```java
public class Solution {
    /**
     * @param nums: an array of Integer
     * @param target: an integer
     * @return: [num1, num2] (num1 < num2)
     */
    public int[] twoSum7(int[] nums, int target) {
        target = Math.abs(target);
        int j = 1;
        for (int i = 0; i < nums.length; i++) {
            j = Math.max(j, i + 1); // prevent i and j overlap
            while (j < nums.length && nums[j] - nums[i] < target) {
                j++;
            }
            if (j >= nums.length) break;
            if (nums[j] - nums[i] == target) {
                // since j is always larger i, thus this order
                return new int[]{nums[i], nums[j]};
            }
        }
        return new int[]{-1, -1};
    }
}
```

### Notes

* This solution is also the two pointers method, but we move the j pointer. We make sure that j is always larger than i, so we do not need to check for the increasing order in the final answer.
* Time complexity: `O(n)`
* Space complexity: `O(1)`
