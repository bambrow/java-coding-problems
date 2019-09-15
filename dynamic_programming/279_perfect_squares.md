# 279 Perfect Squares

```java
/*
Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

For example, given n = 12, return 3 because 12 = 4 + 4 + 4; given n = 13, return 2 because 13 = 4 + 9.
*/

// 这个题虽然有四平方和定理撑腰（任何正整数都可以表示为至多四个数的平方和），然而数学方面的解答太不通用了，脱离了这道题的初衷（虽然数学应该是最快的）。
// 我们还是用动态规划解题。本解法的思路是，对于每一个数字i，不断更新比它大的所有位置所需的最少完全平方数的数量。

class Solution {
    public int numSquares(int n) {
        int[] dp = new int[n+1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;
        for (int i = 0; i <= n; i++) {
            for (int j = 1; i + j*j <= n; j++) {
                dp[i+j*j] = Math.min(dp[i+j*j], dp[i]+1);
            }
        }
        return dp[n];
    }
}

// 也可以使用如下的更新方法，通过i之前的某些位置来计算目前所需的最少完全平方数的数量。

class Solution {
    public int numSquares(int n) {
        int[] dp = new int[n+1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;
        for (int i = 0; i <= n; i++) {
            for (int j = 1; i - j*j >= 0; j++) {
                dp[i] = Math.min(dp[i], dp[i-j*j]+1);
            }
        }
        return dp[n];
    }
}

```

