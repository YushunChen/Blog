---
description: 'ID: 3; medium'
---

# Longest Substring Without Repeating Characters

{% embed url="https://leetcode.com/problems/longest-substring-without-repeating-characters/" %}

## Solution 1

```go
func lengthOfLongestSubstring(s string) int {
    var bitSet [256]bool
    res, left, right := 0, 0, 0
    for left < len(s) {
        if right >= len(s) {
            break
        }
        if bitSet[s[right]] {
            bitSet[s[left]] = false
            left++
        } else {
            bitSet[s[right]] = true
            right++
        }
        if right - left > res {
            res = right - left
        }
    }
    return res
}
```

We use a BitSet to mark if a single character is repeated or not.

