# 72 Edit Distance

```java
/*
Given two words word1 and word2, find the minimum number of steps required to convert word1 to word2. (each operation is counted as 1 step.)

You have the following 3 operations permitted on a word:

a) Insert a character
b) Delete a character
c) Replace a character
*/

// if there is A[1..m] and B[1..n]
// ED(0,0) = 0
// ED(i,0) = i
// ED(0,j) = j
// ED(i,j) = min{ ED(i-1,j-1), ED(i,j-1)+1, ED(i-1,j)+1 }, if A[i] = B[j]
// ED(i,j) = min{ ED(i-1,j-1)+1, ED(i,j-1)+1, ED(i-1,j)+1 }, if A[i] != B[j]
// ED(i,j)表示将A[1..i]编辑到B[1..j]所需要的开销。
// 开脑洞：如果增加，删除和修改所需要的开销不一样，这个题需要怎么修改？
// 我们假设这三个操作分别需要p,q,r的开销。
// ED(0,0) = 0
// ED(i,0) = i*q  因为这是将A[1..i]删光的开销
// ED(0,j) = j*p  因为这是将空字符串变成B[1..j]的开销
// ED(i,j) = min{ ED(i-1,j-1), ED(i,j-1)+p, ED(i-1,j)+q }, if A[i] = B[j]
// ED(i,j) = min{ ED(i-1,j-1)+r, ED(i,j-1)+p, ED(i-1,j)+q }, if A[i] != B[j]

class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        int[][] look = new int[m+1][n+1];
        return ED(word1, word2, m, n, look);
    }
    
    private int ED(String w1, String w2, int i, int j, int[][] look) {
        if (i == 0 && j == 0) return 0;
        if (look[i][j] != 0) return look[i][j];
        if (j == 0) look[i][j] = i;
        else if (i == 0) look[i][j] = j;
        else {
            if (w1.charAt(i-1) == w2.charAt(j-1)) look[i][j] = ED(w1, w2, i-1, j-1, look);
            else look[i][j] = ED(w1, w2, i-1, j-1, look) + 1;
            look[i][j] = Math.min(look[i][j], ED(w1, w2, i-1, j, look) + 1);
            look[i][j] = Math.min(look[i][j], ED(w1, w2, i, j-1, look) + 1);
        }
        return look[i][j];
    }
}
```

