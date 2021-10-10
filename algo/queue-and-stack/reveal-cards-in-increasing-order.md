---
description: ID: 950; medium
---
# Reveal Cards In Increasing Order

{% embed url="https://leetcode.com/problems/reveal-cards-in-increasing-order/" %}

## Solution 1 (Java)

```java
class Solution {
    public int[] deckRevealedIncreasing(int[] deck) {
        Queue<Integer> q = new ArrayDeque<>();
        int[] ans = new int[deck.length];
        for (int i = 0; i < deck.length; i++) {
            q.offer(i);
        }
        Arrays.sort(deck);
        for (int card : deck) {
            ans[q.poll()] = card;
            if (!q.isEmpty()) {
                q.offer(q.poll());
            }
        }
        return ans;
    }
}


// sorted: [2,3,5,7,11,13,17]
// index:  []
// ans:    [2,13,3,11,5,17,7]

//       0   1   2   3   4   5   6
// ans: [2   13  3   11  5   17  7]
```

### Notes

* The queue simulates the deck operations described in the problem.
* We first sort the array and reveal one card, then we put the card after the revealed card to the bottom of the deck (end of queue).
* Time complexity: `O(nlogn)`
