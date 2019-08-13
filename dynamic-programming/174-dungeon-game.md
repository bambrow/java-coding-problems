# 174 Dungeon Game

```java
/*
The demons had captured the princess (P) and imprisoned her in the bottom-right corner of a dungeon. The dungeon consists of M x N rooms laid out in a 2D grid. Our valiant knight (K) was initially positioned in the top-left room and must fight his way through the dungeon to rescue the princess.

The knight has an initial health point represented by a positive integer. If at any point his health point drops to 0 or below, he dies immediately.

Some of the rooms are guarded by demons, so the knight loses health (negative integers) upon entering these rooms; other rooms are either empty (0's) or contain magic orbs that increase the knight's health (positive integers).

In order to reach the princess as quickly as possible, the knight decides to move only rightward or downward in each step.


Write a function to determine the knight's minimum initial health so that he is able to rescue the princess.

For example, given the dungeon below, the initial health of the knight must be at least 7 if he follows the optimal path RIGHT-> RIGHT -> DOWN -> DOWN.

-2 (K)	-3	3
-5	-10	1
10	30	-5 (P)

Notes:

The knight's health has no upper bound.
Any room can contain threats or power-ups, even the first room the knight enters and the bottom-right room where the princess is imprisoned.

*/

// DG(i,j) = 1, if i=m-1 and j=n-1 and d[i][j]>=0
// DG(i,j) = -d[i][j]+1, if i=m-1 and j=n-1 and d[i][j]<0
// DG(i,j) = max{ DG(i,j+1)-d[i][j], 1 }, if i=m-1 and j<n-1
// DG(i,j) = max{ DG(i+1,j)-d[i][j], 1 }, if j=n-1 and i<m-1
// DG(i,j) = max{ min{ DG(i+1,j)-d[i][j], DG(i,j+1)-d[i][j] }, 1 }, if i<m-1 and j<n-1

class Solution {
    public int calculateMinimumHP(int[][] dungeon) {
        if (dungeon.length == 0 || dungeon[0].length == 0) return 1;
        int m = dungeon.length, n = dungeon[0].length;
        int[][] look = new int[m][n];
        return DG(dungeon,m,n,0,0,look);
    } 
    
    private int DG(int[][] d, int m, int n, int i, int j, int[][] look) {
        if (look[i][j] != 0) return look[i][j];
        if (i == m-1 && j == n-1) {
            if (d[i][j] >= 0) look[i][j] = 1;
            else look[i][j] = -d[i][j]+1;
        } else if (i == m-1) {
            look[i][j] = Math.max(DG(d,m,n,i,j+1,look)-d[i][j], 1);
        } else if (j == n-1) {
            look[i][j] = Math.max(DG(d,m,n,i+1,j,look)-d[i][j], 1);
        } else {
            look[i][j] = Math.max(Math.min(DG(d,m,n,i,j+1,look)-d[i][j], DG(d,m,n,i+1,j,look)-d[i][j]), 1);
        }
        return look[i][j];
    }
}

```

