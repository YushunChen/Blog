---
description: ID: 521; easy
---
# Remove Duplicate Numbers in Array

{% embed url="https://www.lintcode.com/problem/521/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param nums: an array of integers
     * @return: the number of unique integers
     */
    public int deduplication(int[] nums) {
        Map<Integer, Boolean> map = new HashMap<>();
        for (int num : nums) {
            map.putIfAbsent(num, true);
        }
        int res = 0;
        for (int key : map.keySet()) {
            nums[res++] = key;
        }
        return res;
    }
}
```

### Notes

* Time complexity: `O(n)`
* Space complexity: `O(n)`

## Solution 2 (Java)

```java
public class Solution {
    /**
     * @param nums: an array of integers
     * @return: the number of unique integers
     */
    public int deduplication(int[] nums) {
        if (nums == null || nums.length == 0)
            return 0;
        Arrays.sort(nums);
        int len = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != nums[len]) {
                nums[++len] = nums[i];
            }
        }
        return len + 1;
    }
}
//                    i
// [1,2,3,4,5,6,3,4,5,6]
//            l
```

### Notes

* Time complexity: `O(nlogn)` from sorting
* Space complexity: `O(n)`
