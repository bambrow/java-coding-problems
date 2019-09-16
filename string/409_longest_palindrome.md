# 409 Longest Palindrome

```java
/*
Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example "Aa" is not considered a palindrome here.

Note:
Assume the length of given string will not exceed 1,010.

Example:

Input:
"abccccdd"

Output:
7

Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.
*/

class Solution {
    public int longestPalindrome(String s) {
        int[] arr = new int[128];
        boolean odd = false;
        int cnt = 0;
        for (int i = 0; i < s.length(); i++) {
            arr[s.charAt(i)]++;
        }
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] % 2 == 0) cnt += arr[i];
            else {
                cnt += arr[i]-1;
                odd = true;
            }
        }
        if (odd) cnt++;
        return cnt;
    }
}
```
