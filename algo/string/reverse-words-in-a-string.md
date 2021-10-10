---
description: ID: 151; medium
---
# Reverse Words in a String

{% embed url="https://leetcode.com/problems/reverse-words-in-a-string/" %}

{% embed url="https://www.lintcode.com/problem/53/" %}

## Solution 1 (Java)

```java
class Solution {
    public String reverseWords(String s) {
        String[] words = s.trim().split("\\s+");
        int end = words.length - 1;
        StringBuffer result = new StringBuffer(words[end]);
        for (int i = end - 1; i >= 0; i--) {
            result.append(" " + words[i]);
        }
        return result.toString();
    }
}
```

## Solution 2 (Java)

```java
class Solution {
    public String reverseWords(String s) {
        if (s == null || s.length() == 0) {
            return "";
        }
        
        String[] words = s.split(" ");
        StringBuffer sb = new StringBuffer();
        
        for (int i = words.length - 1; i >= 0; i--) {
            if (words[i].equals("")) {
                continue;
            }
            if (sb.length() > 0) {
                sb.append(" ");
            }
            sb.append(words[i]);
        }
        return sb.toString();
    }
}
```
