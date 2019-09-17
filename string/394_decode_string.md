# 394 Decode String

```java
/*
Given an encoded string, return it's decoded string.

The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is being repeated exactly k times. Note that k is guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, k. For example, there won't be input like 3a or 2[4].

Examples:

s = "3[a]2[bc]", return "aaabcbc".
s = "3[a2[c]]", return "accaccacc".
s = "2[abc]3[cd]ef", return "abcabccdcdcdef".
*/

class Solution {
    public String decodeString(String s) {
        StringBuilder str = new StringBuilder();
        int i = 0;
        while (i < s.length()) {
            char c = s.charAt(i);
            if (c >= '0' && c <= '9') {
                int j = s.indexOf("[", i);
                int cnt = Integer.parseInt(s.substring(i, j));
                int k = s.indexOf("]", j);
                int helper = s.indexOf("[", j+1);
                while (helper > 0 && helper < k) {
                    k = s.indexOf("]", k+1);
                    helper = s.indexOf("[", helper+1);
                }
                String rep = decodeString(s.substring(j+1, k));
                for (int r = 0; r < cnt; r++) {
                    str.append(rep);
                }
                i = k+1;
            } else {
                str.append(c);
                i++;
            }
        }
        return str.toString();
    }
}
```
