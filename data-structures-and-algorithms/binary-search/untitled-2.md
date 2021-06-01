---
description: 'ID: 600; hard; 包裹黑色像素点的最小矩形'
---

# Smallest Rectangle Enclosing Black Pixels

{% embed url="https://www.lintcode.com/problem/600/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param image: a binary matrix with '0' and '1'
     * @param x: the location of one of the black pixels
     * @param y: the location of one of the black pixels
     * @return: an integer
     */
    public int minArea(char[][] image, int x, int y) {
        if (image == null || image.length == 0 || image[0].length == 0) {
            return -1;
        }

        int row = image.length - 1, col = image[0].length - 1;
        int left = findLeftBound(image, 0, y);
        int right = findRightBound(image, y, col);
        int top = findTopBound(image, 0, x);
        int bottom = findBottomBound(image, x, row);

        return (right - left + 1) * (bottom - top + 1);
    }

    private int findLeftBound(char[][] image, int start, int end) {
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (colHasBlackPixel(image, mid)) {
                end = mid;
            } else {
                start = mid;
            }
        }
        if (colHasBlackPixel(image, start)) {
            return start;
        }
        return end;
    }

    private int findRightBound(char[][] image, int start, int end) {
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (colHasBlackPixel(image, mid)) {
                start = mid;
            } else {
                end = mid;
            }
        }
        if (colHasBlackPixel(image, end)) {
            return end;
        }
        return start;
    }

    private int findTopBound(char[][] image, int start, int end) {
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (rowHasBlackPixel(image, mid)) {
                end = mid;
            } else {
                start = mid;
            }
        }
        if (rowHasBlackPixel(image, start)) {
            return start;
        }
        return end;
    }

    private int findBottomBound(char[][] image, int start, int end) {
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (rowHasBlackPixel(image, mid)) {
                start = mid;
            } else {
                end = mid;
            }
        }
        if (rowHasBlackPixel(image, end)) {
            return end;
        }
        return start;
    }

    private boolean rowHasBlackPixel(char[][] image, int row) {
        for (int i = 0; i < image[0].length; i++) {
            if (image[row][i] == '1') return true;
        }
        return false;
    }
    
    private boolean colHasBlackPixel(char[][] image, int col) {
        for (int i = 0; i < image.length; i++) {
            if (image[i][col] == '1') return true;
        }
        return false;
    }
}
```

### Notes

* We use binary search to find the left, right, top, and bottom boundaries of the black area. Specifically, we are trying to find 1's in these four directions and reduce the range if we cannot. 

