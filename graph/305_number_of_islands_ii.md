# 305 Number of Islands II

```java
/*
A 2d grid map of m rows and n columns is initially filled with water. We may perform an addLand operation which turns the water at position (row, col) into a land. Given a list of positions to operate, count the number of islands after each addLand operation. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example:

Given m = 3, n = 3, positions = [[0,0], [0,1], [1,2], [2,1]].
Initially, the 2d grid grid is filled with water. (Assume 0 represents water and 1 represents land).

0 0 0
0 0 0
0 0 0
Operation #1: addLand(0, 0) turns the water at grid[0][0] into a land.

1 0 0
0 0 0   Number of islands = 1
0 0 0
Operation #2: addLand(0, 1) turns the water at grid[0][1] into a land.

1 1 0
0 0 0   Number of islands = 1
0 0 0
Operation #3: addLand(1, 2) turns the water at grid[1][2] into a land.

1 1 0
0 0 1   Number of islands = 2
0 0 0
Operation #4: addLand(2, 1) turns the water at grid[2][1] into a land.

1 1 0
0 0 1   Number of islands = 3
0 1 0
We return the result as an array: [1, 1, 2, 3]

Challenge:

Can you do it in time complexity O(k log mn), where k is the length of the positions?
*/

class Solution {

    static class UF {

        private int count;
        private int[] parent;
        private int[] rank;

        public UF(int n) {
            parent = new int[n];
            rank = new int[n];
            count = 0;
            for (int i = 0; i < n; i++) {
                parent[i] = -1;
                rank[i] = 0;
            }
        }

        public boolean isIsland(int x) {
            return parent[x] >= 0;
        }

        public void addIsland(int x) {
            parent[x] = x;
            count++;
        }

        public int getCount() {
            return count;
        }

        public int find(int x) {
            if (parent[x] != x) {
                parent[x] = find(parent[x]);
            }
            return parent[x];
        }

        public void union(int x, int y) {
            int rx = find(x);
            int ry = find(y);
            if (rx != ry) {
                if (rank[rx] > rank[ry]) {
                    parent[ry] = rx;
                } else if (rank[rx] < rank[ry]) {
                    parent[rx] = ry;
                } else {
                    parent[ry] = rx;
                    rank[rx]++;
                }
                count--;
            }
        }

    }

    public List<Integer> numIslands2(int m, int n, int[][] positions) {

        List<Integer> list = new LinkedList<>();
        UF uf = new UF(m*n); // union-find

        for (int[] pos : positions) {
            int x = pos[0], y = pos[1];
            int i = x * n + y;
            uf.addIsland(i);
            List<Integer> neighbors = new LinkedList<>();
            if (x > 0 && uf.isIsland((x-1)*n+y)) neighbors.add((x-1)*n+y);
            if (x < m-1 && uf.isIsland((x+1)*n+y)) neighbors.add((x+1)*n+y);
            if (y > 0 && uf.isIsland(x*n+(y-1))) neighbors.add(x*n+(y-1));
            if (y < n-1 && uf.isIsland(x*n+(y+1))) neighbors.add(x*n+(y+1));
            for (int j : neighbors) {
                uf.union(i,j);
            }
            list.add(uf.getCount());
        }

        return list;

    }
}
```
