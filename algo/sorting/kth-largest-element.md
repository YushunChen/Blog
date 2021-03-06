---
description: ID: 5; medium
---
# Kth Largest Element

{% embed url="https://www.lintcode.com/problem/5/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param k: An integer
     * @param nums: An array
     * @return: the Kth largest element
     */
    public int kthLargestElement(int k, int[] nums) {
       return quickSelect(nums, 0, nums.length - 1, k);
    }

    private int quickSelect(int[] nums, int left, int right, int k) {
        int pivot = nums[left];
        int i = left, j = right;
        while (i <= j) {
            while (i <= j && nums[i] > pivot) {
                i++;
            }
            while (i <= j && nums[j] < pivot) {
                j--;
            }
            if (i <= j) {
                int temp = nums[i];
                nums[i++] = nums[j];
                nums[j--] = temp;
            }
        }

        if (left + k - 1 <= j) {
            return quickSelect(nums, left, j, k);
        }
        if (left + k - 1 >= i) {
            return quickSelect(nums, i, right, k - (i - left));
        }
        // special case: j, x, i
        return nums[j + 1];
    }
}

// [9,8,4,2,3]
//        i 
//    j

// pivot = 9, left = 0, right = 4
// pivot = 3, left = 1, right = 4, k = 3 - (1 - 0) = 2
// pivot = 8, left = 1, right = 3, k = 2
// pivot = 2, left = 2, right = 3, k = 2 - (2 - 1) = 1
// pivot = 4, left = 2, right = 2, k = 1
// return nums[j + 1] = 4
```

## Solution 2 (Java)

```java
public class Solution {
    /**
     * @param k: An integer
     * @param nums: An array
     * @return: the Kth largest element
     */
    public int kthLargestElement(int k, int[] nums) {
        if (nums == null || nums.length == 0 || nums.length < k || k < 1)
            return -1;
        // convert the problem to the (n-k)th smallest element
        k = nums.length - k;
        return partition(nums, 0, nums.length - 1, k);
    }

    private int partition(int[] nums, int start, int end, int k) {
        if (start >= end) return nums[k];
        int left = start, right = end;
        int pivot = nums[left + (right - left) / 2];
        while (left <= right) {
            while (left <= right && nums[left] < pivot) {
                left++;
            }
            while (left <= right && nums[right] > pivot) {
                right--;
            }
            if (left <= right) {
                int temp = nums[left];
                nums[left++] = nums[right];
                nums[right--] = temp;
            }
        }
        if (k <= right) return partition(nums, start, right, k);
        if (k >= left) return partition(nums, left, end, k);
        return nums[k];
    }


}
```

### Notes

* Updated version of [Solution 1](kth-largest-element.md#solution-1-java). Easier to understand and write.
