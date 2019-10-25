# 59 Spiral Matrix II

```java
/*
Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.

For example,
Given n = 3,

You should return the following matrix:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
*/

// 类似54。

class Solution {

    public int[][] generateMatrix(int n) {
        int[][] arr = new int[n][n];
        int topX = 0, botX = n-1;
        int i = 1;
        while (topX <= botX) {
            if (topX == botX) {
                arr[topX][topX] = i++;
            } else {
                int x = topX, y = topX;
                while (y < botX) arr[topX][y++] = i++;
                while (x < botX) arr[x++][botX] = i++;
                while (y > topX) arr[botX][y--] = i++;
                while (x > topX) arr[x--][topX] = i++;
            }
            topX++;
            botX--;
        }
        return arr;
    }

}
```
