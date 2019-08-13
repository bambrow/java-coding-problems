# 338 Counting Bits

```java
/*
Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

Example:
For num = 5 you should return [0,1,1,2,1,2].

Follow up:

It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass?
Space complexity should be O(n).
Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.

*/

// 注释掉的解法：
// look[1] = look[0] + 1
// look[2..3] = look[0..1] + 1
// look[4..7] = look[0..3] + 1
// look[8..15] = look[0..7] + 1
// look[2^i..(2^(i+1))-1] = look[0..(2^i)-1] + 1
// 原因很简单，上述所有式子（除第一个）中，左边的数字二进制均为右边的数字二进制最前面加了一个1。
// 下面讲一个更聪明的递推解法：
// look[i] = look[i/2] + i%2
// 这个解法的确聪明，但是我一时半会是想不出来的。我短时间只能想到被注释的解法。

class Solution {
    
    public int[] countBits(int num) {
        int[] look = new int[num+1];
        for (int i = 1; i < num+1; i++) {
            look[i] = look[i/2] + i%2;
        }
        return look;
    }
    
    /*
    public int[] countBits(int num) {
        int[] look = new int[num+1];
        int k = 1;
        for (int i = 1; i < num+1; i++) {
            if (k*2 == i) k *= 2;
            look[i] = look[i-k] + 1;
        }
        return look;
    }
    */
}
```

