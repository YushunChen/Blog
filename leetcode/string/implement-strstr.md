---
description: 'ID: 28; easy'
---

# Implement strStr\(\)

{% embed url="https://leetcode.com/problems/implement-strstr/" %}

## Solution 1

```go
func strStr(haystack string, needle string) int {
    ln, lh := len(needle), len(haystack)
    if ln == 0 {
        return 0
    }
    if ln > lh {
        return -1
    }
    for i,_ := range haystack {
        if haystack[i] == needle[0] && i+ln <= lh && haystack[i+ln-1] == needle[ln-1] {
            if haystack[i:i+ln] == needle {
                return i
            }
        }
    }
    return -1
}
```

## Solution 2

```go
func strStr(haystack string, needle string) int {
    for i := 0; ; i++ {
        for j := 0; ; j++ {
            if j == len(needle) {
                return i
            }
            if i+j == len(haystack) {
                return -1
            }
            if needle[j] != haystack[i+j] {
                break
            }
        }
    }
}

// haystack = "hello", needle = "ll"
// i: 0 1 2 2 2
// j: 0 0 0 1 2
```

## Solution 3

```go
import "strings"

func strStr(haystack string, needle string) int {
    return strings.Index(haystack, needle)
}
```

{% hint style="info" %}
Not really a "solution"...
{% endhint %}

