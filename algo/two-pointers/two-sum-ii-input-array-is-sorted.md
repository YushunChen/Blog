---
description: 'ID: 167; easy'
---

# Two Sum II - Input array is sorted

{% embed url="https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/" %}

{% embed url="https://www.lintcode.com/problem/608/" %}

## Solution 1 \(Go\)

```go
func twoSum(numbers []int, target int) []int {
    res := make([]int, 0)
    for i := 0; i < len(numbers); i++ {
        for j := i + 1; j < len(numbers); j++ {
            if numbers[i] + numbers[j] == target {
                res = append(res, i+1, j+1)
                return res
            }
        }
    }
    return res
}
```

## Solution 2 \(Go\)

```go
func twoSum(numbers []int, target int) []int {
    m := make(map[int]int)
    for i,v := range numbers {
        j := target - v
        if _, ok := m[j]; ok {
            return []int{m[j]+1, i+1}
        }
        m[v] = i
    }
    return nil
}
```

## Solution 3 \(Go\)

```go
func twoSum(numbers []int, target int) []int {
    p1, p2 := 0, len(numbers)-1
    // less than since cannot use the same element twice
    for p1 < p2 {
        sum := numbers[p1] + numbers[p2]
        if sum == target {
            return []int{p1+1, p2+1}
        } else if sum < target {
            p1++
        } else {
            p2--
        }
    }
    return nil
}
```

## Solution 4 \(Java\)

```java
public class Solution {
    /**
     * @param nums: an array of Integer
     * @param target: target = nums[index1] + nums[index2]
     * @return: [index1 + 1, index2 + 1] (index1 < index2)
     */
    public int[] twoSum(int[] nums, int target) {
        if (nums == null || nums.length == 0)
            return null;
        int left = 0, right = nums.length - 1;
        while (left < right) {
            if (nums[left] + nums[right] == target)
                return new int[]{left + 1, right + 1};
            else if (nums[left] + nums[right] < target)
                left++;
            else
                right--;
        }
        return null;
    }
}
```

### Notes

* Here we sufficiently use the condition that the array is sorted.

