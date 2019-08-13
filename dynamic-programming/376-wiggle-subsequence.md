# 376 Wiggle Subsequence

```java
/*
A sequence of numbers is called a wiggle sequence if the differences between successive numbers strictly alternate between positive and negative. The first difference (if one exists) may be either positive or negative. A sequence with fewer than two elements is trivially a wiggle sequence.

For example, [1,7,4,9,2,5] is a wiggle sequence because the differences (6,-3,5,-7,3) are alternately positive and negative. In contrast, [1,4,7,2,5] and [1,7,4,5,5] are not wiggle sequences, the first because its first two differences are positive and the second because its last difference is zero.

Given a sequence of integers, return the length of the longest subsequence that is a wiggle sequence. A subsequence is obtained by deleting some number of elements (eventually, also zero) from the original sequence, leaving the remaining elements in their original order.

Examples:
Input: [1,7,4,9,2,5]
Output: 6
The entire sequence is a wiggle sequence.

Input: [1,17,5,10,13,15,10,5,16,8]
Output: 7
There are several subsequences that achieve this length. One is [1,17,10,13,10,16,8].

Input: [1,2,3,4,5,6,7,8,9]
Output: 2
Follow up:
Can you do it in O(n) time?
*/

// 解法非常明晰：首先跳过开头的相同数字，找到第一个不同数。然后判断初始条件，是需要向上的数还是向下的数。
// 如果到了这一步，初始答案从2开始。对于每一个新数，做如下事情：
// 如果需要向上的数，而且该数确实大于last，则更新答案，更新需求，更新last；
// 如果需要向上的数，但该数小于等于last，就把last更新成当前数；
// 如果需要向下的数，而且该数确实小于last，则更新答案，更新需求，更新last；
// 如果需要向下的数，但该数大于等于last，就把last更新成当前数。
// 可以简化一下for中的if，让行数少一些。见第二段代码。

class Solution {
    public int wiggleMaxLength(int[] nums) {
        int l = nums.length;
        if (l <= 1) return l;
        int k = 0;
        while (k < l-1 && nums[k] == nums[k+1]) k++;
        if (k == l-1) return 1;
        int last = nums[k+1];
        boolean up = nums[k+1] < nums[k];
        int cnt = 2;
        for (int i = k+1; i < l-1; i++) {
            if (up && nums[i+1] > last) {
                cnt++;
                up = !up;
                last = nums[i+1];
            } else if (up && nums[i+1] <= last) {
                last = nums[i+1];
            } else if (!up && nums[i+1] < last) {
                cnt++;
                up = !up;
                last = nums[i+1];
            } else if (!up && nums[i+1] >= last) {
                last = nums[i+1];
            }
        }
        return cnt;
    }
}

class Solution {
    public int wiggleMaxLength(int[] nums) {
        int l = nums.length;
        if (l <= 1) return l;
        int k = 0;
        while (k < l-1 && nums[k] == nums[k+1]) k++;
        if (k == l-1) return 1;
        int last = nums[k+1];
        boolean up = nums[k+1] < nums[k];
        int cnt = 2;
        for (int i = k+1; i < l-1; i++) {
            if ((up && nums[i+1] > last) || (!up && nums[i+1] < last)) {
                cnt++;
                up = !up;
            }
            last = nums[i+1];
        }
        return cnt;
    }
}


```

