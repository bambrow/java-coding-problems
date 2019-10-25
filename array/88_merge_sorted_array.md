# 88 Merge Sorted Array

```java
/*
Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.
*/

// 该题的过程是从后往前的。nums1有足够的空间容纳所有数。
// k初始指向m+n-1，也就是最大下标，最大值存储的位置。
// 归并结束后，如果i仍旧大于等于0，则可以不做任何事；但如果j仍旧大于等于0，证明nums2数组还没复制完，应该继续复制nums2。

class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m-1, j = n-1, k = m+n-1;
        while (i >= 0 && j >= 0) {
            nums1[k] = nums1[i] > nums2[j] ? nums1[i] : nums2[j];
            if (nums1[i] > nums2[j]) i--;
            else j--;
            k--;
        }
        while (j >= 0) {
            nums1[k] = nums2[j];
            k--; j--;
        }
    }
}

// 以下是原解法，简单一些但是略微难读。

class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m-1, j = n-1, k = m+n-1;
        while (i >= 0 && j >= 0) nums1[k--] = (nums1[i] > nums2[j]) ? nums1[i--] : nums2[j--];
        while (j >= 0) nums1[k--] = nums2[j--];
    }
}
```
