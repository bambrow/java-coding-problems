# 189 Rotate Array

```java
/*
Rotate an array of n elements to the right by k steps.

For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].

Note:
Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.

[show hint]

Hint:
Could you do it in-place with O(1) extra space?
Related problem: Reverse Words in a String II
*/

// 先翻转后k个数字，再翻转前面n-k个数字，再全部翻转，即可得到答案。

class Solution {
    public void rotate(int[] nums, int k) {
        k %= nums.length;
        if (k == 0) return;
        reverse(nums, nums.length-k, nums.length-1);
        reverse(nums, 0, nums.length-k-1);
        reverse(nums, 0, nums.length-1);
    }

    private void reverse(int[] nums, int i, int j) {
        while (i<j) {
            int temp = nums[i];
            nums[i] = nums[j];
            nums[j] = temp;
            i++;
            j--;
        }
    }
}

// 自己想出来的解法。首先寻找数组长度和k的最大公约数。
// 这个最大公约数就是要替换的轮数，不过这里要注意各种边界条件。
// 随后进行替换，每一轮从下标i开始，不断替换(i+k)%n的数，直到回到i为止。
// 替换完全部轮数后，数组即转换完毕。

class Solution {
    public void rotate(int[] nums, int k) {
        if (k <= 0) return;
        if (nums.length <= 1) return;
        int n = nums.length;
        k %= n;
        if (k == 0) return;
        int round = gcd(n, k);
        for (int i = 0; i < round; i++) {
            int j = i;
            int init = nums[j];
            while ((j + k) % n != i) {
                int temp = nums[(j+k)%n];
                nums[(j+k)%n] = init;
                init = temp;
                j = (j + k) % n;
            }
            nums[i] = init;
        }
    }
    private int gcd(int n, int k) {
        if (n % k == 0) return k;
        else return gcd(k, n%k);
    }
}

```
