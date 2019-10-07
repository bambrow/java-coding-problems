# 74 Search a 2D Matrix

```java
/*
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.
For example,

Consider the following matrix:

[
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
Given target = 3, return true.
*/

// 从右上角开始寻找。
// 比较当前数与目标的关系：如果相等，返回true。
// 如果当前数更大，因为矩阵每一列都排好序，证明当前列中处于当前位置下方的数只会更大，没必要在这一列寻找了。因此前移一列。
// 如果当前数更小，因为矩阵每一行都排好序，证明当前行中处于当前位置左侧的数只会更小，没必要在这一行寻找了，因此下移一行。
// 重复步骤直到越界。

class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix.length == 0 || matrix[0].length == 0) return false;
        int row = 0;
        int col = matrix[0].length-1;
        while (row < matrix.length && col >= 0) {
            if (matrix[row][col] == target) return true;
            else if (matrix[row][col] > target) col--;
            else row++;
        }
        return false;
    }
}
```
