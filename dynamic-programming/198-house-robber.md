# 198 House Robber

```java
/*
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

*/

// 看到没有，这年头抢劫犯都开始学算法了，不忍直视啊！
// 这道题很简单，递推如下：
// HR(0) = 0, HR(1) = house(1)
// HR(l) = max{ HR(l-1), HR(l-2) + house(l) }
// 自顶向下的解法。自底向上的递推解法（带look数组）被注释掉了，因为超时了。
// 其实还可以进一步简化，摒弃look数组，直接用三个数循环计算。

class Solution {
    
    public int rob(int[] nums) {
        int l = nums.length;
        if (l == 0) return 0;
        int[] look = new int[l+1];
        look[1] = nums[0];
        for (int i = 2; i < l+1; i++) {
            look[i] = Math.max(look[i-1], look[i-2] + nums[i-1]);
        }
        return look[l];
    }
    
    /*
    public int rob(int[] nums) {
        int l = nums.length;
        int[] look = new int[l];
        return HR(nums, l, look);
    }

    private int HR(int[] nums, int l, int[] look) {
        if (l == 0) return 0;
        if (l == 1) return nums[0];
        if (look[l-1] != 0) return look[l-1];
        look[l-1] = Math.max(HR(nums, l-1, look), HR(nums, l-2, look) + nums[l-1]);
        return look[l-1];
    }
    */
}
```

