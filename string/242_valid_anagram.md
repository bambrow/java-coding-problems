# 242 Valid Anagram

```java
/*
Given two strings s and t, write a function to determine if t is an anagram of s.

For example,
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.

Note:
You may assume the string contains only lowercase alphabets.
*/


public class Solution {
    public boolean isAnagram(String s, String t) {
        int[] freq = new int[26];
        for (int i = 0; i < s.length(); i++) {
            freq[s.charAt(i)-'a']++;
        }
        for (int i = 0; i < t.length(); i++) {
            freq[t.charAt(i)-'a']--;
            if (freq[t.charAt(i)-'a'] < 0) return false;
        }
        for (int k : freq) {
            if (k != 0) return false;
        }
        return true;
    }
}
```
