---
description: ID: 28; easy; 搜索二维矩阵
---
# Search a 2D Matrix

{% embed url="https://www.lintcode.com/problem/28/" %}

## Solution 1 (Java)

```java
public class Solution {
    /**
     * @param matrix: matrix, a list of lists of integers
     * @param target: An integer
     * @return: a boolean, indicate whether matrix contains target
     */
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }

        int row = matrix.length, col = matrix[0].length;
        int start = 0, end = row * col - 1;
        
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            int midNum = matrix[mid / col][mid % col];
            if (midNum == target) {
                return true;
            } else if (midNum < target) {
                start = mid;
            } else {
                end = mid;
            }
        }

        if (matrix[start / col][start % col] == target) return true;
        if (matrix[end / col][end % col] == target) return true;
        return false;
    }
}
```
