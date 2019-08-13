# 85 Maximal Rectangle

```java
/*
Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

For example, given the following matrix:

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
Return 6.
*/

// 本题参考84。解法与84类似，给出的辅助方法与84完全相同。
// 我们把矩阵看作一个直方图。
// 如果从最后一行往上看，我们可以看到高度为4，0，0，3，0的直方图（只要遇到0高度就是0）。
// 从倒数第二行看，则会看到3，1，3，2，2的直方图。
// 我们从上到下扫描矩阵每一行，构建直方图的高度。比如上图的例子：
// 第一行的高度为10100，第二行为20211，第三行为31322，第四行为40030。
// 我们发现这样的构建方法可以得到从任意一行向上看的直方图高度。
// 原则是遇到0，那么高度清零；否则高度+1。这样的话我们就完全把矩阵转换成了以每一行为基准的直方图。
// 求直方图的最大区域问题，已经在84里解决了。

class Solution {
    public int maximalRectangle(char[][] matrix) {
        
        if (matrix.length == 0 || matrix[0].length == 0) return 0;
        
        int m = matrix.length, n = matrix[0].length;
        int[][] heights = new int[m][n];
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == '0') heights[i][j] = 0;
                else heights[i][j] = i == 0 ? 1 : heights[i-1][j]+1;
            }
        }
        
        int max = 0;
        for (int i = 0; i < m; i++) {
            max = Math.max(max, largestRectangleArea(heights[i]));
        }
        
        return max;
        
    }
    
    public int largestRectangleArea(int[] heights) {
        
        Stack<Integer> s = new Stack<>();
        int max = 0;
        for (int i = 0; i <= heights.length; ) {
            int h = i == heights.length ? 0 : heights[i];
            if (s.isEmpty() || h > heights[s.peek()]) {
                s.push(i);
                i++;
            } else {
                int t = s.pop();
                max = Math.max(max, heights[t] * (s.isEmpty() ? i : i-1-s.peek()));
            }
        }
        
        return max;
        
    }
}
```

