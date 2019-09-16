# 35 Search Insert Position

```java
/*
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Here are few examples.
[1,3,5,6], 5 → 2
[1,3,5,6], 2 → 1
[1,3,5,6], 7 → 4
[1,3,5,6], 0 → 0
*/

// 简单题，二分查找即可。若数存在则返回index，若不存在则返回数组里大于target的最小值的index。

class Solution {
    public int searchInsert(int[] nums, int target) {
        int lo = 0, hi = nums.length - 1;
        while (lo <= hi) {
            int mid = lo + (hi-lo)/2;
            if (target == nums[mid]) return mid;
            if (target > nums[mid]) lo = mid+1;
            else hi = mid-1;
        }
        return lo;
    }
}
```
