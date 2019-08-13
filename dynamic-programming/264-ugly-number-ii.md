# 264 Ugly Number II

```java
/*
Write a program to find the n-th ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.

Note that 1 is typically treated as an ugly number, and n does not exceed 1690.
*/

// 本题原本想着的是O(nlogn)解法，结果仔细一想还是存在O(n)解法的。
// 用i，j，k维护三个下标，表示2，3，5倍数的位置。例如，如果i，j，k三个位置的数字为x，y，z，那么下一个值一定会在2x，3y，5z中产生。
// 在这个数产生之后，要把i，j，k都更新一遍，因为有可能2x=3y=5z，或者任意两者相等，如果不更新就会出现重复。

class Solution {
    public int nthUglyNumber(int n) {
        if (n <= 0) return 0;
        List<Integer> look = new ArrayList<>();
        look.add(1);
        int i = 0, j = 0, k = 0;
        while (look.size() < n) {
            int next = Math.min(look.get(i)*2, Math.min(look.get(j)*3, look.get(k)*5));
            look.add(next);
            if (next == look.get(i)*2) i++;
            if (next == look.get(j)*3) j++;
            if (next == look.get(k)*5) k++;
        }
        return look.get(look.size()-1);
    }
}
```

