# 54 Spiral Matrix

```java
/*
Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:

[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
You should return [1,2,3,6,9,8,7,4,5].
*/

// 类似题目适合使用圈式处理方法，从最外圈处理到最里圈。
// 注意各种边界条件。

class Solution {

    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> list = new ArrayList<>();
        if (matrix.length == 0) return list;
        int topX = 0, topY = 0;
        int botX = matrix.length - 1, botY = matrix[0].length - 1;
        while (topX <= botX && topY <= botY) {
            processRing(matrix, list, topX++, topY++, botX--, botY--);
        }
        return list;
    }

    private void processRing(int[][] matrix, List<Integer> list, int topX, int topY, int botX, int botY) {
        if (topX == botX) {
            for (int i = topY; i <= botY; i++) {
                list.add(matrix[topX][i]);
            }
        } else if (topY == botY) {
            for (int j = topX; j <= botX; j++) {
                list.add(matrix[j][topY]);
            }
        } else {
            int x = topX, y = topY;
            while (y < botY) list.add(matrix[x][y++]);
            while (x < botX) list.add(matrix[x++][y]);
            while (y > topY) list.add(matrix[x][y--]);
            while (x > topX) list.add(matrix[x--][y]);
        }
    }

}

```
