# 213 House Robber II

```java
/*
Note: This is an extension of House Robber.

After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention. This time, all houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, the security system for these houses remain the same as for those in the previous street.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.
*/

// 198改版，房子首尾相连。
// 方法类似，使用辅助方法circleRob来计算[i,j]区间的最佳值。然后将此方法应用到[0,l-2]与[1,l-1]即可。
// 辅助方法内部采用三数循环计算。

class Solution {
    public int rob(int[] nums) {
        int l = nums.length;
        if (l == 0) return 0;
        if (l == 1) return nums[0];
        return Math.max(circleRob(nums, 0, l-2), circleRob(nums, 1, l-1));
    }

    private int circleRob(int[] nums, int i, int j) {
        int x = 0, y = nums[i], z = nums[i];
        for (int k = i+1; k <= j; k++) {
            z = Math.max(y, x + nums[k]);
            x = y;
            y = z;
        }
        return z;
    }
}
```

