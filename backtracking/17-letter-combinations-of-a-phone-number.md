# 17 Letter Combinations of a Phone Number

```java
/*
Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below.



Input:Digit string "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
Note:
Although the above answer is in lexicographical order, your answer could be in any order you want.
*/

// 还是类似39/40/77的解法。这里需要强调一点就是DFS函数内部的改动。这里与之前的题目有些不同，因为我们有一个lookup数组来做查找用，要首先通过当前的字符找到lookup数组的index，然后遍历这个index下的所有可能。下一层采用的层数是level+1，因为我们只是想单纯地考察下一个字符。这与以上三个题目皆有不同。

class Solution {
    public List<String> letterCombinations(String digits) {
        List<String> ans = new ArrayList<>();
        if (digits.length() == 0) return ans;
        String[] lookup = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        StringBuilder cur = new StringBuilder();
        DFS(digits, 0, ans, lookup, cur);
        return ans;
    }
    
    public void DFS(String digits, int level, List<String> ans, String[] lookup, StringBuilder cur) {
        if (level == digits.length()) {
            ans.add(cur.toString());
            return;
        }
        int index = digits.charAt(level) - '0';
        for (int i = 0; i < lookup[index].length(); i++) {
            cur.append(lookup[index].charAt(i));
            DFS(digits, level+1, ans, lookup, cur);
            cur.deleteCharAt(cur.length()-1);
        }
    }
}
```

