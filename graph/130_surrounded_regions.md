# 130 Surrounded Regions

```java
/*
Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

For example,
X X X X
X O O X
X X O X
X O X X
After running your function, the board should be:

X X X X
X X X X
X X X X
X O X X

*/

class Solution {
    public void solve(char[][] board) {
        if (board.length < 2 || board[0].length < 2) return;
        int m = board.length, n = board[0].length;
        for (int i = 0; i < m; i++) {
            if (board[i][0] == 'O') {
                DFS(board, i, 0, m, n);
            }
            if (board[i][n-1] == 'O') {
                DFS(board, i, n-1, m, n);
            }
        }
        for (int j = 0; j < n; j++) {
            if (board[0][j] == 'O') {
                DFS(board, 0, j, m, n);
            }
            if (board[m-1][j] == 'O') {
                DFS(board, m-1, j, m, n);
            }
        }
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == 'N') {
                    board[i][j] = 'O';
                } else if (board[i][j] == 'O') {
                    board[i][j] = 'X';
                }
            }
        }
    }
    private void DFS(char[][] board, int i, int j, int m, int n) {
        board[i][j] = 'N';
        if (i > 0 && board[i-1][j] == 'O') {
            DFS(board, i-1, j, m, n);
        }
        if (i < m-1 && board[i+1][j] == 'O') {
            DFS(board, i+1, j, m, n);
        }
        if (j > 0 && board[i][j-1] == 'O') {
            DFS(board, i, j-1, m, n);
        }
        if (j < n-1 && board[i][j+1] == 'O') {
            DFS(board, i, j+1, m, n);
        }
    }
}
```
