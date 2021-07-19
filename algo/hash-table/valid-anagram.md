---
description: 'ID: 242; easy'
---

# Valid Anagram

{% embed url="https://leetcode.com/problems/valid-anagram/" %}

{% embed url="https://www.lintcode.com/problem/158/" %}

## Solution 1 \(Java\)

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        int sLen = s.length(), tLen = t.length();
        if (sLen == 0 || tLen == 0 || sLen != tLen) return false;
        int[] sMap = new int[256];
        int[] tMap = new int[256];
        for (int i = 0; i < sLen; i++) {
            sMap[s.charAt(i)]++;
            tMap[t.charAt(i)]++;
        }
        for (int i = 0; i < sMap.length; i++) {
            if (sMap[i] != tMap[i])
                return false;
        }
        return true;
    }
}
```

