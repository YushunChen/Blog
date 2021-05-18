---
description: 'ID: 88; easy'
---

# Merge Sorted Array

{% embed url="https://leetcode.com/problems/merge-sorted-array/" %}

## 1st Solution

```go
func merge(nums1 []int, m int, nums2 []int, n int)  {
    // i is the index of the result array (filling backwards)
    for i := m+n; m > 0 && n > 0; i-- {
        if nums1[m-1] > nums2[n-1] {
            nums1[i-1] = nums1[m-1]
            m--
        } else {
            nums1[i-1] = nums2[n-1]
            n--
        }
    }
    for n > 0 {
        nums1[n-1] = nums2[n-1]
        n--
    }
}
```

