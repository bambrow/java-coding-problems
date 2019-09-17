# 200 Number of Islands

```java
/*
Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:

11110
11010
11000
00000
Answer: 1

Example 2:

11000
11000
00100
00011
Answer: 3
*/

class Solution {
    public int numIslands(char[][] grid) {
        if (grid.length == 0) return 0;
        int num = 0;
        int m = grid.length, n = grid[0].length;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == '1') {
                    num++;
                    grid[i][j] = '0';
                    Queue<int[]> queue = new LinkedList<>();
                    queue.offer(new int[] {i,j});
                    while (!queue.isEmpty()) {
                        int[] coor = queue.poll();
                        int x = coor[0], y = coor[1];
                        if (x > 0 && grid[x-1][y] == '1') {
                            queue.offer(new int[] {x-1,y});
                            grid[x-1][y] = '0'; // set to '0' must be inside the if block!
                        }
                        if (x < m-1 && grid[x+1][y] == '1') {
                            queue.offer(new int[] {x+1,y});
                            grid[x+1][y] = '0';
                        }
                        if (y > 0 && grid[x][y-1] == '1') {
                            queue.offer(new int[] {x,y-1});
                            grid[x][y-1] = '0';
                        }
                        if (y < n-1 && grid[x][y+1] == '1') {
                            queue.offer(new int[] {x,y+1});
                            grid[x][y+1] = '0';
                        }
                    }
                }
            }
        }
        return num;
    }
}
```
