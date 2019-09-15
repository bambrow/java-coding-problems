# 516 Longest Palindromic Subsequence

```java
/*
Given a string s, find the longest palindromic subsequence's length in s. You may assume that the maximum length of s is 1000.

Example 1:
Input:

"bbbab"
Output:
4
One possible longest palindromic subsequence is "bbbb".
Example 2:
Input:

"cbbd"
Output:
2
One possible longest palindromic subsequence is "bb".
*/

// LPS(i,j) = 0, if i > j
// LPS(i,j) = 1, if i = j
// LPS(i,j) = 2 + LPS(i+1,j-1), if s[i] = s[j]
// LPS(i,j) = max{ LPS(i+1,j), LPS(i,j-1) }, otherwise

class Solution {
    public int longestPalindromeSubseq(String s) {
        if (s == null || s.length() == 0) return 0;
        int l = s.length();
        int[][] look = new int[l][l];
        return LPS(s, 0, l-1, look);
    }

    private int LPS(String s, int i, int j, int[][] look) {
        if (look[i][j] != 0) return look[i][j];
        if (i > j) look[i][j] = 0;
        else if (i == j) look[i][j] = 1;
        else if (s.charAt(i) == s.charAt(j)) look[i][j] = 2 + LPS(s, i+1, j-1, look);
        else look[i][j] = Math.max(LPS(s, i+1, j, look), LPS(s, i, j-1, look));
        return look[i][j];
    }
}
```

