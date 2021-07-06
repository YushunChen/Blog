---
description: 'ID: 662; easy; 猜数游戏'
---

# Guess Number Higher or Lower

{% embed url="https://www.lintcode.com/problem/662/" %}

## Solution 1 \(Java\)

```java
/* The guess API is defined in the parent class GuessGame.
   @param num, your guess
   @return -1 if my number is lower, 1 if my number is higher, otherwise return 0
      int guess(int num); */

public class Solution extends GuessGame {
    /**
     * @param n an integer
     * @return the number you guess
     */
    public int guessNumber(int n) {
        final int CORRECT = 0, GUESS_SMALLER = -1, GUESS_LARGER = 1;
        int left = 1, right = n;
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (guess(mid) == CORRECT) {
                return mid;
            } else if (guess(mid) == GUESS_SMALLER) {
                right = mid;
            } else { // (guess(mid) == GUESS_LARGER)
                left = mid;
            }
        }

        if (guess(left) == CORRECT) return left;
        if (guess(right) == CORRECT) return right;
        return 0;
    }
}
```

### Notes

* This is almost the same as [classical binary search](classical-binary-search.md).

