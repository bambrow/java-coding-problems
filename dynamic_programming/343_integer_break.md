# 343 Integer Break

```java
/*
Given a positive integer n, break it into the sum of at least two positive integers and maximize the product of those integers. Return the maximum product you can get.

For example, given n = 2, return 1 (2 = 1 + 1); given n = 10, return 36 (10 = 3 + 3 + 4).

Note: You may assume that n is not less than 2 and not larger than 58.
*/

// IB(1) = 1
// IB(i) = max{ max{ j, IB(j) }, max{ i-j, IB(i-j) } } for all j+j <= i

class Solution {
    public int integerBreak(int n) {
        int[] look = new int[n+1];
        look[1] = 1;
        for (int i = 2; i < n+1; i++) {
            for (int j = 1; j <= i/2; j++) {
                look[i] = Math.max(look[i], Math.max(j, look[j]) * Math.max(i-j, look[i-j]));
            }
        }
        return look[n];
    }
}
```

