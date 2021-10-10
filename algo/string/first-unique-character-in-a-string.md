---
description: ID: 209; easy
---
# First Unique Character in a String

{% embed url="https://www.lintcode.com/problem/209/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param str: str: the given string
     * @return: char: the first unique character in a given string
     */
    public char firstUniqChar(String str) {
        if (str == null || str.length() == 0)
            return '0';
        int[] map = new int[256];
        for (int i = 0; i < str.length(); i++) {
            map[str.charAt(i)]++;
        }
        for (int i = 0; i < str.length(); i++) {
            if (map[str.charAt(i)] == 1)
                return str.charAt(i);
        }
        return '0';
    }
}
```
