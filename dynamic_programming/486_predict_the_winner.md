# 486 Predict the Winner

```java
/*
Given an array of scores that are non-negative integers. Player 1 picks one of the numbers from either end of the array followed by the player 2 and then player 1 and so on. Each time a player picks a number, that number will not be available for the next player. This continues until all the scores have been chosen. The player with the maximum score wins.

Given an array of scores, predict whether player 1 is the winner. You can assume each player plays to maximize his score.

Example 1:
Input: [1, 5, 2]
Output: False
Explanation: Initially, player 1 can choose between 1 and 2.
If he chooses 2 (or 1), then player 2 can choose from 1 (or 2) and 5. If player 2 chooses 5, then player 1 will be left with 1 (or 2).
So, final score of player 1 is 1 + 2 = 3, and player 2 is 5.
Hence, player 1 will never be the winner and you need to return False.
Example 2:
Input: [1, 5, 233, 7]
Output: True
Explanation: Player 1 first chooses 1. Then player 2 have to choose between 5 and 7. No matter which number player 2 choose, player 1 can choose 233.
Finally, player 1 has more score (234) than player 2 (12), so you need to return True representing player1 can win.
Note:
1 <= length of the array <= 20.
Any scores in the given array are non-negative integers and will not exceed 10,000,000.
If the scores of both players are equal, then player 1 is still the winner.
*/

// 暴力递归。竟然没超时，表示很惊讶。APick返回某玩家在先选数字的时候可以得到的分数。BPick返回某玩家在后选数字的时候可以得到的分数。APick函数中，既然自己选，那么必然是越大越好！然后他就变成了后选，所以APick递归调用BPick。BPick函数中，受制于人，对方先选，对方肯定留下最差的！然后他就变成了先选，所以BPick递归调用APick。

class Solution {
    public boolean PredictTheWinner(int[] nums) {
        int AScore = APick(nums, 0, nums.length-1);
        int BScore = BPick(nums, 0, nums.length-1);
        if (AScore >= BScore) return true;
        else return false;
    }

    private int APick(int[] nums, int i, int j) {
        if (i == j) return nums[i];
        return Math.max(nums[i] + BPick(nums, i+1, j), nums[j] + BPick(nums, i, j-1));
    }

    private int BPick(int[] nums, int i, int j) {
        if (i == j) return 0;
        return Math.min(APick(nums, i+1, j), APick(nums, i, j-1));
    }
}

// 优化，使用数组保存答案。

class Solution {
    public boolean PredictTheWinner(int[] nums) {
        int l = nums.length;
        int[][] A = new int[l][l];
        int[][] B = new int[l][l];
        int AScore = APick(nums, 0, l-1, A, B);
        int BScore = BPick(nums, 0, l-1, A, B);
        if (AScore >= BScore) return true;
        else return false;
    }

    private int APick(int[] nums, int i, int j, int[][] A, int[][] B) {
        if (A[i][j] != 0) return A[i][j];
        if (i == j) A[i][j] = nums[i];
        else {
            int first = nums[i] + BPick(nums, i+1, j, A, B);
            int last = nums[j] + BPick(nums, i, j-1, A, B);
            if (first > last) A[i][j] = first;
            else A[i][j] = last;
        }
        return A[i][j];
    }

    private int BPick(int[] nums, int i, int j, int[][] A, int[][] B) {
        if (B[i][j] != 0) return B[i][j];
        if (i == j) B[i][j] = 0;
        else {
            int first = APick(nums, i+1, j, A, B);
            int last = APick(nums, i, j-1, A, B);
            if (first < last) B[i][j] = first;
            else B[i][j] = last;
        }
        return B[i][j];
    }
}

// 终极优化，不过我觉得还是上面的版本亲民。

class Solution {
    public boolean PredictTheWinner(int[] nums) {
        int l = nums.length;
        int[][] A = new int[l][l];
        int[][] B = new int[l][l];
        for (int j = 0; j < l; j++) {
            A[j][j] = nums[j];
            for (int i = j-1; i >= 0; i--) {
                A[i][j] = Math.max(nums[i] + B[i+1][j], nums[j] + B[i][j-1]);
                B[i][j] = Math.min(A[i+1][j], A[i][j-1]);
            }
        }
        return A[0][l-1] >= B[0][l-1];
    }
}


```
