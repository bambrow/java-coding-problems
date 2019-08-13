# 494 Target Sum

```java
/*
You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols + and -. For each integer, you should choose one from + and - as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.

Example 1:
Input: nums is [1, 1, 1, 1, 1], S is 3. 
Output: 5
Explanation: 

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

There are 5 ways to assign symbols to make the sum of nums be target 3.
Note:
The length of the given array is positive and will not exceed 20.
The sum of elements in the given array will not exceed 1000.
Your output answer is guaranteed to be fitted in a 32-bit integer.
*/

// TS(S,0) = 2, if S = nums[0] and nums[0] = 0
// TS(S,0) = 1, if S = nums[0] or S = -nums[0], and nums[0] != 0
// TS(S,0) = 0, if S != nums[0] and S != -nums[0]
// TS(S,i) = 
//    TS(S-nums[i], i-1) + TS(S+nums[i], i-1), if S-nums[i] >= -sum and S+nums[i] <= sum
//    TS(S-nums[i], i-1), if S-nums[i] >= -sum and S+nums[i] > sum
//    TS(S+nums[i], i-1), if S-nums[i] < -sum and S+nums[i] <= sum
// 上面递推的下标是-sum..sum，实际使用下标是0..2*sum
// 两者之间的关系为：S = j-sum;  j = S+sum
// 其中S为目标加和，j为对应的数组下标。在TS函数中，内部的S相当于上一行的j。

class Solution {
    public int findTargetSumWays(int[] nums, int S) {
        int sum = 0;
        for (int k : nums) sum += k;
        if (S > sum || S < -sum) return 0;
        int[][] look = new int[2*sum+1][nums.length];
        return TS(S+sum, nums.length-1, nums, look, sum);
    }
    
    private int TS(int S, int i, int[] nums, int[][] look, int sum) {
        if (look[S][i] != 0) return look[S][i];
        if (i == 0) {
            if (S == nums[i] + sum) look[S][i]++;
            if (S == -nums[i] + sum) look[S][i]++;
        }
        else {
            if (S-nums[i] >= 0) look[S][i] += TS(S-nums[i], i-1, nums, look, sum);
            if (S+nums[i] <= 2*sum) look[S][i] += TS(S+nums[i], i-1, nums, look, sum);
        }
        return look[S][i];
    }
}

```

