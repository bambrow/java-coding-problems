# 152 Maximum Product Subarray

```java
/*
Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array [2,3,-2,4],
the contiguous subarray [2,3] has the largest product = 6.
*/

// 本题不同于53的一点是，负数乘以负数会变成正数。所以需要维护当前的最大值与最小值，最小值可能为负数，但是如果下一步乘以了一个负数，就可以变成最大值了。
// 于是动态方程可能是这样的：
// maxDP[i+1] = max(maxDP[i]*nums[i+1], nums[i+1], minDP[i]*nums[i+1])
// minDP[i+1] = min(minDP[i]*nums[i+1], nums[i+1], maxDP[i]*nums[i+1])
// dp[i+1] = max(dp[i], maxDP[i+1])
// 其中前两者存储了现在的乘积最大值与最小值（相当于maxNow与minNow），而dp存储了历史最大值。
// 放入nums[i+1]的意义是在i处数值可能为0，那么maxDP[i]与minDP[i]会全数变成0，在i+1处需要重新开始计算。

class Solution {
    public int maxProduct(int[] nums) {
        if (nums.length == 0) return 0;
        int maxSoFar = nums[0], minProd = nums[0], maxProd = nums[0];
        for (int i = 1; i < nums.length; i++) {
            int maxProdTemp = maxProd;
            maxProd = Math.max(Math.max(maxProd*nums[i], nums[i]), minProd*nums[i]);
            minProd = Math.min(Math.min(maxProdTemp*nums[i], nums[i]), minProd*nums[i]);
            maxSoFar = Math.max(maxSoFar, maxProd);
        }
        return maxSoFar;
    }
}
```

