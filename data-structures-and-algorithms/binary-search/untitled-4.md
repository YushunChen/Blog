---
description: 'ID: 38; medium; 搜索二维矩阵（二）'
---

# Search a 2D Matrix II

{% embed url="https://www.lintcode.com/problem/38/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param matrix: A list of lists of integers
     * @param target: An integer you want to search in matrix
     * @return: An integer indicate the total occurrence of target in the given matrix
     */
    public int searchMatrix(int[][] matrix, int target) {
        int row = 0, col = matrix[0].length - 1;
        int targetCount = 0;
        while (row < matrix.length && col >= 0) {
            if (matrix[row][col] == target) {
                targetCount++;
                row++;
                col--;
            } else if (matrix[row][col] < target) {
                row++;
            } else {
                col--;
            }
        }
        return targetCount;
    }
}
```

### Notes

* We pick a special number in the 2D matrix here. Either the **top right** element or the **bottom left** element will work. The reason is that we want to reduce the range in which we research for the `target`. In the code above, we chose the top right element and it is the largest in its row but the smallest in its column. Thus, if the `target` is larger than it, we proceed downward to find it; if the `target` is smaller than it, we proceed to the left. And if the `target` is equal to it, we increment the `targetCounter` and move diagonally since each number is unique in its row and column.

