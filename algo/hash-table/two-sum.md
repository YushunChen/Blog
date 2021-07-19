---
description: 'ID: 1; Easy'
---

# Two Sum

{% embed url="https://leetcode.com/problems/two-sum/" %}

{% embed url="https://www.lintcode.com/problem/56/" %}

## Solution 1 \(Go\)

```go
func twoSum(nums []int, target int) []int {
    var indices []int
    for i := 0; i < len(nums)-1; i++ {
        for j := i+1; j < len(nums) ; j++ {
            if nums[i] + nums[j] == target {
                indices = append(indices, i, j)
            }
        }
    }
    return indices
}
```

## Solution 2 \(Go\)

```go
func twoSum(nums []int, target int) []int {
    m := make(map[int]int)
    for i,v := range nums {
        j := target - v
        if _, ok := m[j]; ok {
            return []int{m[j], i}
        }
        m[v] = i
    }
    return nil
}
```

## Solution 3 \(Java\)

```java
public class Solution {
    /**
     * @param numbers: An array of Integer
     * @param target: target = numbers[index1] + numbers[index2]
     * @return: [index1, index2] (index1 < index2)
     */
    public int[] twoSum(int[] numbers, int target) {
        // <number, its index>
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < numbers.length; i++) {
            int j = target - numbers[i];
            if (map.containsKey(j)) {
                return new int[]{map.get(j), i};
            }
            map.put(numbers[i], i);
        }
        return null;
    }
}
```

