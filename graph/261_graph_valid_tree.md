# 261 Graph Valid Tree

```java
/*
Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.

For example:

Given n = 5 and edges = [[0, 1], [0, 2], [0, 3], [1, 4]], return true.

Given n = 5 and edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]], return false.

Note: you can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.

*/

class Solution {
    public boolean validTree(int n, int[][] edges) {
        if (edges.length != n-1) return false;
        int[] parent = new int[n];
        Arrays.fill(parent, -1);
        for (int[] edge : edges) {
            int x = edge[0];
            int y = edge[1];
            add(parent, x);
            add(parent, y);
            if (!union(parent, x, y)) return false;
        }
        return true;
    }
    private void add(int[] parent, int x) {
        if (parent[x] == -1) parent[x] = x;
    }
    private int find(int[] parent, int x) {
        if (parent[x] != x) {
            parent[x] = find(parent, parent[x]);
        }
        return parent[x];
    }
    private boolean union(int[] parent, int x, int y) {
        int rx = find(parent, x);
        int ry = find(parent, y);
        if (rx == ry) return false;
        parent[ry] = rx;
        return true;
    }
}
```
