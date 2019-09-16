# 266 Palindrome Permutation

```java
/*
Given a string, determine if a permutation of the string could form a palindrome.

For example,
"code" -> False, "aab" -> True, "carerac" -> True.
*/

class Solution {
    public boolean canPermutePalindrome(String s) {
        int[] arr = new int[128];
        int cnt = 0;
        for (int i = 0; i < s.length(); i++) {
            arr[s.charAt(i)]++;
            if (arr[s.charAt(i)] % 2 == 1) cnt++;
            else cnt--;
        }
        return cnt <= 1;
    }
}
```
