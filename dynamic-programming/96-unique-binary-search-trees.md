# 96 Unique Binary Search Trees

```java
/*
Given n, how many structurally unique BST's (binary search trees) that store values 1...n?

For example,
Given n = 3, there are a total of 5 unique BST's.

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
*/

// 学习了FA之后有感，重做！
// UT(i,k) = sum{ UT(i,j-1) * UT(j+1,k) }, for all i <= j <= k
// UT(i,k) = 1, if i >= k
// 二维数组方法见注释掉的代码。
// 以上是二维数组。一维行不行呢？当然可以！
// UT(k) = sum{ UT(j-1) * UT(k-j-1) }, for all 0 <= j <= k
// UT(k) = 1, if k <= 0

class Solution {
    
    public int numTrees(int n) {
        if (n == 0) return 0;
        int[] look = new int[n];
        return UT(n-1, look);
    }
    
    private int UT(int k, int[] look) {
        if (k <= 0) return 1;
        if (look[k] != 0) return look[k];
        for (int j = 0; j <= k; j++) {
            look[k] += UT(j-1,look) * UT(k-j-1,look);
        }
        return look[k];
    }
    
    /*
    public int numTrees(int n) {
        if (n == 0) return 0;
        int[][] look = new int[n][n];
        return UT(0, n-1, look);
    }
    
    private int UT(int i, int k, int[][] look) {
        if (i >= k) return 1;
        if (look[i][k] != 0) return look[i][k];
        for (int j = i; j <= k; j++) {
            look[i][k] += UT(i,j-1,look) * UT(j+1,k,look);
        }
        return look[i][k];
    }
    */
}

// 本题注意一定要满足BST的性质。即：左子树小于根节点，右子树大于根节点。
// 假设某子树根节点为i，那么左子树一定小于i，也就是[0,i-1]；右子树一定大于i，也就是[i+1,n]。
// 假设左子树与右子树的节点给定，左子树有x种排列方式，右子树有y种，那么以i为根节点的子树总排列方式为x*y。
// 然而节点有多种可能，所以要把所有可能的x*y全部加和。
// 则可以得dp方程：dp[i] = sum(dp[k] * dp[i-k-1]) for all k in [0,i)
// 本题选择构建n+1大小的数组，是因为有可能某子树没有一个节点。这种情况也应该考虑在内，而且种类数为1。

class Solution {
    public int numTrees(int n) {
        if (n == 0) return 0;
        int[] dp = new int[n+1];
        dp[0] = 1;
        dp[1] = 1;
        for (int i = 2; i <= n; i++) {
            for (int j = 0; j < i; j++) {
                dp[i] += dp[j] * dp[i-j-1];
            }
        }
        return dp[n];
    }
}
```

