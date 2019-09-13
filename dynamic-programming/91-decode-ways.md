# 91 Decode Ways

```java
/*
A message containing letters from A-Z is being encoded to numbers using the following mapping:

'A' -> 1
'B' -> 2
...
'Z' -> 26
Given an encoded message containing digits, determine the total number of ways to decode it.

For example,
Given encoded message "12", it could be decoded as "AB" (1 2) or "L" (12).

The number of ways decoding "12" is 2.
*/

// 采用FA老爷子的自底向上方法。其实改写成自顶向下很容易，不过时间紧迫，先不做了。
// 字符串的题太烦了！看看这不忍直视的边界条件，我不想说啥了，慢慢看吧。
// 基本理念就是：
// ND(l) = if 1 = 0 then 1; if l = 1 then check s[0], if 0 then 0, else 1
// ND(l) = ND(l-1)+ND(l-2), if s[l-1..l] is between 11-19, 21-26
// ND(l) = ND(l-2), if s[l-1..l] is 10 or 20
// ND(l) = ND(l-1), if s[l-1..l] is 01-09, 27-99 (except 30, 40, 50, 60, 70, 80, 90)
// ND(l) = 0, if s[l-1..l] is 00, 30, 40, 50, 60, 70, 80, 90

class Solution {
    public int numDecodings(String s) {
        if (s == null || s.length() == 0) return 0;
        int l = s.length();
        int[] look = new int[l+1];
        for (int i = 0; i < l+1; i++) look[i] = -1;
        return ND(s,l,look);
    }

    private int ND(String s, int l, int[] look) {
        if (l == 0) return 1;
        if (l == 1) return s.charAt(0) == '0' ? 0 : 1;
        if (look[l] != -1) return look[l];
        if (s.charAt(l-1) == '0') {
            if (s.charAt(l-2) == '1' || s.charAt(l-2) == '2') look[l] = ND(s,l-2,look);
            else look[l] = 0;
        } else {
            if (s.charAt(l-2) == '0') look[l] = ND(s,l-1,look);
            else if ((s.charAt(l-2) == '2' && s.charAt(l-1) <= '6') || (s.charAt(l-2) == '1' && s.charAt(l-1) <= '9'))
                look[l] = ND(s,l-1,look) + ND(s,l-2,look);
            else look[l] = ND(s,l-1,look);
        }
        return look[l];
    }
}
```

