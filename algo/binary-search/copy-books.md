---
description: ID: 437; medium; 书籍复印
---
# Copy Books

{% embed url="https://www.lintcode.com/problem/437/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param pages: an array of integers
     * @param k: An integer
     * @return: an integer
     */
    public int copyBooks(int[] pages, int k) {
        if (pages == null || pages.length == 0 || k <= 0)
            return 0;
        
        int left = 0, right = Integer.MAX_VALUE;

        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (isTimeFeasible(pages, k, mid)) {
                right = mid;
            } else {
                left = mid;
            }
        }

        return isTimeFeasible(pages, k, left) ? left : right;
    }

    private boolean isTimeFeasible(int[] pages, int k, int time) {
        int numOfCopiers = 0, remain = 0;
        for (int page : pages) {
            if (page > time) return false;
            if (page > remain) {
                numOfCopiers++;
                remain = time;
            }
            remain -= page;
        }
        return numOfCopiers <= k;
    }
}
```

### Notes

* The check of a feasible time here is crucial. Given a `time`, how do we know the minimum number of copiers needed to complete the job?
  * If there is one book that takes longer than `time` to be copied, there is no way this `time` is feasible.
  * Else in the general case, count the minimum number of copier needed. If this minimum number is larger than `k`, then the `time` is not feasible.

## Solution 2 (Java)

```java
public class Solution {
    /**
     * @param pages: an array of integers
     * @param k: An integer
     * @return: an integer
     */
    public int copyBooks(int[] pages, int k) {
        if (pages == null || pages.length == 0 || k <= 0)
            return 0;
        
        int left = pages[0], right = 0, mid;
        for (int page : pages) {
            left = Math.max(left, page);
            right += page;
        }

        while (left + 1 < right) {
            mid = left + (right - left) / 2;
            if (isTimeFeasible(pages, k, mid)) {
                right = mid;
            } else {
                left = mid;
            }
        }

        return isTimeFeasible(pages, k, left) ? left : right;
    }

    private boolean isTimeFeasible(int[] pages, int k, int time) {
        int numOfCopiers = 1, pageSum = 0;
        for (int page : pages) {
            if (page > time) return false;
            if (pageSum + page <= time) {
                pageSum += page;
            } else {
                numOfCopiers++;
                pageSum = page;
            }
        }
        
        return numOfCopiers <= k;
    }
}
```

### Notes

* We can further reduce the initial range by setting `left` to be the maximum page number and `right` to be the sum of the `pages` array. The reason is that the lower bound of the time is achieved by having `k = pages.length` and each person copies one book; the minimum time now would be the time to copy the book with largest page count. Then, the upper bound of the time is achieved by having only 1 copier to copy all the books by himself; so the time would be the sum of all the pages counts.
* Also, this solution uses a slightly different method to determine if time is feasible.
