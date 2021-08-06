---
description: 'ID: 364; hard'
---

# Trapping Rain Water II

{% embed url="https://www.lintcode.com/problem/364/" %}

## Solution 1 \(Java\)

```java
public class Solution {

    private class Cell {
        int x, y, h;
        public Cell(int x, int y, int h) {
            this.x = x;
            this.y = y;
            this.h = h;
        }
    }

    /**
     * @param heights: a matrix of integers
     * @return: an integer
     */
    public int trapRainWater(int[][] heights) {
        if (heights == null || heights.length == 0)
            return 0;
        PriorityQueue<Cell> minHeap = new PriorityQueue<>(new Comparator<Cell>() {
            public int compare(Cell a, Cell b) {
                return a.h - b.h;
            }
        });
        int n = heights.length, m = heights[0].length; // n = 5, m = 4
        boolean[][] visited = new boolean[n][m];

        for (int i = 0; i < n; i++) {
            minHeap.offer(new Cell(i, 0, heights[i][0]));
            minHeap.offer(new Cell(i, m - 1, heights[i][m - 1]));
            visited[i][0] = true;
            visited[i][m - 1] = true;
        }
        for (int i = 0; i < m; i++) {
            minHeap.offer(new Cell(0, i, heights[0][i]));
            minHeap.offer(new Cell(n - 1, i, heights[n - 1][i]));
            visited[0][i] = true;
            visited[n - 1][i] = true;
        }

        int water = 0;
        int[] dx = {1, 0, -1, 0};
        int[] dy = {0, 1, 0, -1};
        while (!minHeap.isEmpty()) {
            Cell curr = minHeap.poll();
            for (int i = 0; i < 4; i++) {
                int nx = curr.x + dx[i];
                int ny = curr.y + dy[i];
                if (0 <= nx && nx < n && 0 <= ny && ny < m && !visited[nx][ny]) {
                    visited[nx][ny] = true;
                    if (curr.h > heights[nx][ny]) {
                        water += curr.h - heights[nx][ny];
                        minHeap.offer(new Cell(nx, ny, curr.h));
                    } else {
                        minHeap.offer(new Cell(nx, ny, heights[nx][ny]));
                    }
                    // minHeap.offer(new Cell(nx, ny, Math.max(curr.h, heights[nx][ny])));
                    // water = water + Math.max(0, curr.h - heights[nx][ny]);
                }
            }
        }
        return water;
    }
}
```

