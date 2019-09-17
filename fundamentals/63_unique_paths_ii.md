# 63 Unique Paths II

```java
/*
Follow up for "Unique Paths":

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

For example,
There is one obstacle in the middle of a 3x3 grid as illustrated below.

[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
The total number of unique paths is 2.

Note: m and n will be at most 100.
*/

// O(n) space

class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if (obstacleGrid.length == 0 || obstacleGrid[0].length == 0) return 0;
        int m = obstacleGrid.length, n = obstacleGrid[0].length;
        int[] look = new int[n];
        look[0] = obstacleGrid[0][0] == 1 ? 0 : 1;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (obstacleGrid[i][j] == 1) {
                    look[j] = 0;
                } else if (j > 0) {
                    look[j] = look[j] + look[j-1];
                }
            }
        }
        return look[look.length-1];
    }
}


// O(mn) space

class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if (obstacleGrid.length == 0 || obstacleGrid[0].length == 0) return 0;
        int m = obstacleGrid.length, n = obstacleGrid[0].length;
        int[][] look = new int[m][n];
        look[0][0] = (obstacleGrid[0][0] == 0) ? 1 : 0;
        for (int i = 1; i < m; i++) {
            look[i][0] = (obstacleGrid[i][0] == 0 && look[i-1][0] == 1) ? 1 : 0;
        }
        for (int j = 1; j < n; j++) {
            look[0][j] = (obstacleGrid[0][j] == 0 && look[0][j-1] == 1) ? 1 : 0;
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                look[i][j] = (obstacleGrid[i][j] == 1) ? 0 : look[i-1][j]+look[i][j-1];
            }
        }
        return look[m-1][n-1];
    }
}

// 62改进版。机器人遇到障碍无法通过。
// 那么我们的dp矩阵也应该做一些改动。首先对于（0，0）点，如果有障碍，机器人可以歇菜了，整个地图哪里都不能去。这时候我们把这个点设置成0。否则设置成1。
// 初始化第一行第一列。首先行列这里我们知道，由于机器人只能向右向下，如果某个点有障碍，那么这个点之后都去不了了。比如（i，0）有障碍，那么（i，0）一直到（m，0）机器人全都无法抵达。第一行的情况同理。
// 那么在构建中间行列的过程中，如果某个点有障碍，就设置为0；否则依旧是原公式。
// 这种设计也可以保证在（0，0）这个点有障碍时，整个矩阵全都是0。

class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if (obstacleGrid.length == 0 || obstacleGrid[0].length == 0) return 0;
        int m = obstacleGrid.length, n = obstacleGrid[0].length;
        int[][] dp = new int[m][n];
        dp[0][0] = (obstacleGrid[0][0] == 0) ? 1 : 0;
        for (int i = 1; i < m; i++) {
            dp[i][0] = (obstacleGrid[i][0] == 0 && dp[i-1][0] == 1) ? 1 : 0;
        }
        for (int j = 1; j < n; j++) {
            dp[0][j] = (obstacleGrid[0][j] == 0 && dp[0][j-1] == 1) ? 1 : 0;
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = (obstacleGrid[i][j] == 1) ? 0 : dp[i-1][j]+dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
}
```
