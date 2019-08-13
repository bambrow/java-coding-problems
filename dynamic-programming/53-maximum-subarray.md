# 53 Maximum Subarray

```java
/*
Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.

click to show more practice.

More practice:
If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.
*/

// Kadane算法。摘自维基百科：扫描一次整个数列的所有数值，在每一个扫描点计算以该点数值为结束点的子数列的最大和（正数和）。该子数列由两部分组成：以前一个位置为结束点的最大子数列、该位置的数值。因为该算法用到了“最佳子结构”（以每个位置为终点的最大子数列都是基于其前一位置的最大子数列计算得出），该算法可看成动态规划的一个例子。

class Solution {
    public int maxSubArray(int[] nums) {
        int maxSoFar = nums[0], maxNow = nums[0];
        for (int i = 1; i < nums.length; i++) {
            maxNow = Math.max(maxNow+nums[i], nums[i]);
            maxSoFar = Math.max(maxSoFar, maxNow);
        }
        return maxSoFar;
    }
}

// 也可以用经典动态规划求解。
// for循环内的第三行，如果当前加和小于0，重置了当前加和为0。这是因为计算最大值不可能会把之前的负值也加上，起码要从0开始。

class Solution {
    public int maxSubArray(int[] nums) {
        int sumNow = 0, maxSum = Integer.MIN_VALUE;
        for (int num: nums) {
            sumNow += num;
            maxSum = Math.max(maxSum, sumNow);
            sumNow = sumNow < 0 ? 0 : sumNow;
        }
        return maxSum;
    }
}


```

