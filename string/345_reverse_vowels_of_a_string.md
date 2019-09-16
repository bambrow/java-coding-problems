# 345 Reverse Vowels of a String

```java
/*
Write a function that takes a string as input and reverse only the vowels of a string.

Example 1:
Given s = "hello", return "holle".

Example 2:
Given s = "leetcode", return "leotcede".

Note:
The vowels does not include the letter "y".
*/

class Solution {
    public String reverseVowels(String s) {
        char[] cs = s.toCharArray();
        int i = 0, j = cs.length-1;
        while (i < j) {
            while (i < j && !isVowel(cs[i])) i++;
            while (j > i && !isVowel(cs[j])) j--;
            char temp = cs[i]; cs[i] = cs[j]; cs[j] = temp;
            i++; j--;
        }
        return new String(cs);
    }

    private boolean isVowel(char c) {
        if (c < 'a') c = (char) (c - 'A' + 'a');
        if (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u') return true;
        return false;
    }
}
```
