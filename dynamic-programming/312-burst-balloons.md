# 312 Burst Balloons

```java
/*
Given n balloons, indexed from 0 to n-1. Each balloon is painted with a number on it represented by array nums. You are asked to burst all the balloons. If the you burst balloon i you will get nums[left] * nums[i] * nums[right] coins. Here left and right are adjacent indices of i. After the burst, the left and right then becomes adjacent.

Find the maximum coins you can collect by bursting the balloons wisely.

Note: 
(1) You may imagine nums[-1] = nums[n] = 1. They are not real therefore you can not burst them.
(2) 0 ≤ n ≤ 500, 0 ≤ nums[i] ≤ 100

Example:

Given [3, 1, 5, 8]

Return 167

    nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []
   coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167


*/

class Solution {
    public int maxCoins(int[] nums) {
        if (nums.length == 0) return 0;
        int[] arr = new int[nums.length + 2];
        int n = 0;
        for (int x : nums) {
            if (x > 0) {
                arr[++n] = x;
            }
        }
        arr[0] = arr[++n] = 1;
        int[][] look = new int[n+1][n+1];
        return BB(arr, 0, n, look);
    }
    private int BB(int[] arr, int i, int j, int[][] look) {
        if (look[i][j] > 0) return look[i][j];
        if (j <= i + 1) return 0;
        int max = 0;
        for (int x = i+1; x < j; x++) {
            max = Math.max(max, (BB(arr, i, x, look) + arr[i] * arr[x] * arr[j] + BB(arr, x, j, look)));
        }
        look[i][j] = max;
        return look[i][j];
    }
}
```

