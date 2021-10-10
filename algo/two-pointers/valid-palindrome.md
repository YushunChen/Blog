---
description: ID: 415; medium
---
# Valid Palindrome

{% embed url="https://www.lintcode.com/problem/415/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param s: A string
     * @return: Whether the string is a valid palindrome
     */
    public boolean isPalindrome(String s) {
        if (s == null || s.length() == 0)
            return true;
        int left = 0, right = s.length() - 1;
        char[] c = s.toCharArray();
        while (left < right) {
            while (left < right && !Character.isLetterOrDigit(c[left])) {
                left++;
            }
            while (left < right && !Character.isLetterOrDigit(c[right])) {
                right--;
            }
            char leftChar = Character.toLowerCase(c[left]);
            char rightChar = Character.toLowerCase(c[right]);
            if (leftChar != rightChar)
                return false;
            left++;
            right--;
        }
        return true;
    }
}
```

## Solution 2 (Java)

```java
public class Solution {
    /**
     * @param s: A string
     * @return: Whether the string is a valid palindrome
     */
    public boolean isPalindrome(String s) {
        if (s == null) return true;
        s = s.toLowerCase();
        int left = 0, right = s.length() - 1;
        while (left < right) {
            if (!Character.isLetterOrDigit(s.charAt(left))) {
                left++;
                continue;
            }
            if (!Character.isLetterOrDigit(s.charAt(right))) {
                right--;
                continue;
            }
            if (s.charAt(left) != s.charAt(right))
                return false;
            left++;
            right--;
        }
        return true;
    }
}
```
