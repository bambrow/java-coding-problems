# 62 Unique Paths

```java
/*
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?


Above is a 3 x 7 grid. How many possible unique paths are there?

Note: m and n will be at most 100.
*/

// O(min(m,n)) space

class Solution {
    public int uniquePaths(int m, int n) {
        int[] look = m >= n ? new int[n] : new int[m];
        Arrays.fill(look, 1);
        for (int k = 1; k < Math.max(m, n); k++) {
            for (int i = 1; i < look.length; i++) {
                look[i] = look[i] + look[i-1];
            }
        }
        return look[look.length-1];
    }
}


// O(mn) space

class Solution {
    public int uniquePaths(int m, int n) {
        int[][] look = new int[m][n];
        for (int i = 0; i < m; i++) {
            look[i][0] = 1;
        }
        for (int j = 0; j < n; j++) {
            look[0][j] = 1;
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                look[i][j] = look[i-1][j] + look[i][j-1];
            }
        }
        return look[m-1][n-1];
    }
}

// 经典动态规划。对于任意点（i，j），机器人要到达这个点，必须首先到达（i-1，j）或者（i，j-1）。
// 因此（i，j）的路径数就是（i-1，j）与（i，j-1）路径数的加和。
// 于是得到dp[i][j] = dp[i-1][j] + dp[i][j-1]
// 其中dp[i][j]表示（0，0）到（i，j）的路径数。
// 不难看出，对于任意的i或者j，[i][0]与[0][j]都只能是1（第一列与第一行），因为机器人只能向右或向下走。

class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        for (int i = 0; i < m; i++) {
            dp[i][0] = 1;
        }
        for (int j = 0; j < n; j++) {
            dp[0][j] = 1;
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
}
```
