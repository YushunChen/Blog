---
description: ID; 74; medium; 第一个错误的代码版本
---

# First Bad Version

{% embed url="https://www.lintcode.com/problem/74/" %}

## Solution 1 \(Java\)

```java
/**
 * public class SVNRepo {
 *     public static boolean isBadVersion(int k);
 * }
 * you can use SVNRepo.isBadVersion(k) to judge whether 
 * the kth code version is bad or not.
*/
public class Solution {
    /**
     * @param n: An integer
     * @return: An integer which is the first bad version.
     */
    public int findFirstBadVersion(int n) {
        int left = 1, right = n;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            boolean isBad = SVNRepo.isBadVersion(mid);
            if (isBad) {
                right = mid;
            } else {
                left = mid;
            }
        }

        if (SVNRepo.isBadVersion(left)) return left;
        if (SVNRepo.isBadVersion(right)) return right;
        return 0;
    }
}
```

