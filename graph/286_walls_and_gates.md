# 286 Walls and Gates

```java
/*
You are given a m x n 2D grid initialized with these three possible values.

-1 - A wall or an obstacle.
0 - A gate.
INF - Infinity means an empty room. We use the value 2^31 - 1 = 2147483647 to represent INF as you may assume that the distance to a gate is less than 2147483647.
Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with INF.

For example, given the 2D grid:
INF  -1  0  INF
INF INF INF  -1
INF  -1 INF  -1
  0  -1 INF INF
After running your function, the 2D grid should be:
  3  -1   0   1
  2   2   1  -1
  1  -1   2  -1
  0  -1   3   4

*/

class Solution {
    public void wallsAndGates(int[][] rooms) {
        if (rooms.length == 0 || rooms[0].length == 0) return;
        int m = rooms.length, n = rooms[0].length;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (rooms[i][j] == 0) {
                    DFS(rooms, i, j, 0, m, n);
                }
            }
        }
    }
    private void DFS(int[][] rooms, int i, int j, int dist, int m, int n) {
        int d = dist + 1;
        if (i > 0 && rooms[i-1][j] > d) {
            rooms[i-1][j] = d;
            DFS(rooms, i-1, j, d, m, n);
        }
        if (i < m-1 && rooms[i+1][j] > d) {
            rooms[i+1][j] = d;
            DFS(rooms, i+1, j, d, m, n);
        }
        if (j > 0 && rooms[i][j-1] > d) {
            rooms[i][j-1] = d;
            DFS(rooms, i, j-1, d, m, n);
        }
        if (j < n-1 && rooms[i][j+1] > d) {
            rooms[i][j+1] = d;
            DFS(rooms, i, j+1, d, m, n);
        }
    }
}
```
