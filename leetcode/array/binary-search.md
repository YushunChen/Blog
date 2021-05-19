# Binary Search

{% embed url="https://leetcode.com/problems/binary-search/" %}

## 1st Solution

```go
func search(nums []int, target int) int {
    low, high := 0, len(nums) - 1
    for low <= high {
        mid := (low + high) / 2
        if nums[mid] == target {
            return mid
        } else if nums[mid] > target {
            high = mid - 1
        } else {
            low = mid + 1
        }
    }
    return -1
}
```

