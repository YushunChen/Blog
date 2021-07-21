---
description: 'ID: 401; medium'
---

# Kth Smallest Number in Sorted Matrix

{% embed url="https://www.lintcode.com/problem/401/" %}

## Solution 1 \(Java\)

```java
public class Solution {

    class Pair {
        int x, y, val;
        public Pair(int x, int y, int val) {
            this.x = x;
            this.y = y;
            this.val = val;
        }
    }
    /**
     * @param matrix: a matrix of integers
     * @param k: An integer
     * @return: the kth smallest number in the matrix
     */
    public int kthSmallest(int[][] matrix, int k) {
        int[] dx = {0, 1};
        int[] dy = {1, 0};
        int n = matrix.length, m = matrix[0].length;
        boolean[][] visited = new boolean[n][m];
        Queue<Pair> minHeap = new PriorityQueue<>(new Comparator<Pair>() {
            public int compare(Pair p1, Pair p2) {
                return p1.val - p2.val;
            }
        });
        minHeap.offer(new Pair(0, 0, matrix[0][0]));

        for (int i = 0; i < k - 1; i++) {
            Pair curr = minHeap.poll();
            for (int j = 0; j < 2; j++) {
                int next_x = curr.x + dx[j];
                int next_y = curr.y + dy[j];
                if (next_x < n && next_y < m && !visited[next_x][next_y]) {
                    Pair next = new Pair(next_x, next_y, matrix[next_x][next_y]);
                    minHeap.offer(next);
                    visited[next_x][next_y] = true;
                }
            }
        }
        return minHeap.peek().val;
    }
}
```

### Notes

* We use a **min heap** to keep track of the numbers. This solution is essentially a BFS. Starting from the top left number, which is the minimum number in the matrix, then we add the number on its right and the number below it. 
* We poll the min heap `k - 1` times and eventually we end up with the kth smallest number in the heap.
* It is also important to keep track of which numbers are already visited, just like what is down in graph traversal problems;
* Time complexity: `O(klogn)`

## Solution 2 \(Java\)

```java
public class Solution {

    class Result {
        boolean exists;
        int rank;
        public Result(boolean e, int r) {
            exists = e;
            rank = r;
        }
    }
    /**
     * @param matrix: a matrix of integers
     * @param k: An integer
     * @return: the kth smallest number in the matrix
     */
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length, m = matrix[0].length;
        int left = matrix[0][0];
        int right = matrix[n - 1][m - 1];
        while (left <= right) {
            int mid = left + (right - left) / 2;
            Result res = check(mid, matrix);
            if (res.exists && res.rank == k) {
                return mid;
            } else if (res.rank < k) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return left;
    }

    private Result check(int value, int[][] matrix) {
        int n = matrix.length, m = matrix[0].length;
        int i = n - 1, j = 0;
        Result res = new Result(false, 0);
        while (i >= 0 && j < m) {
            if (matrix[i][j] == value)
                res.exists = true;
            if (matrix[i][j] <= value) {
                res.rank += i + 1;
                j += 1;
            } else {
                i -= 1;
            }
        }
        return res;
    }

    
}
```

### Notes

* Using the sorted property, it is natural to think about **binary search**. 

