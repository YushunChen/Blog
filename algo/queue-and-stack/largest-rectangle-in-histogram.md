---
description: 'ID: 122; hard'
---

# Largest Rectangle in Histogram

{% embed url="https://www.lintcode.com/problem/122/" %}

## Solution 1 \(Java\)

```java
public class Solution {
    /**
     * @param height: A list of integer
     * @return: The area of largest rectangle in the histogram
     */
    public int largestRectangleArea(int[] height) {
        if (height == null || height.length == 0)
            return 0;
        int maxArea = 0;
        Deque<Integer> stack = new ArrayDeque<>();
        for (int i = 0; i <= height.length; i++) {
            int curr = i == height.length ? -1 : height[i];
            while (!stack.isEmpty() && curr <= height[stack.peek()]) {
                int target = stack.pop();
                int h = height[target];
                int w = stack.isEmpty() ? i : i - stack.peek() - 1;
                maxArea = Math.max(maxArea, h * w);
            }
            stack.push(i);
        }
        return maxArea;
    }
}

//       |   
//     | |    
//     | |    
//     | |   |
// |   | | | |
// | | | | | |

// i = 6: cur = -1; target = 1, h = 1, w = 6, ans = 10
// stack = []
```

### Notes

* We used a non-decreasing stack in this solution. Each time before we push the element into the stack, we pop out the elements that are larger than it. Then, each time when the element is popped from the stack, we know the first element to its left that is smaller than it \(top of the stack\) and the first element to its right that is smaller than it \(element to be pushed\). So, we can calculate the area squeezed by these two elements, which is `h * w`. This is the maximum area reached by stretching the element to be popped to its left and right \(restrained by elements that are smaller than it to its left and right\).
* Because we need to calculate the width \(`w`\), instead of pushing the actual elements, we push the indices to the stack.

