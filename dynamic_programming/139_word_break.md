# 139 Word Break

```java
/*
Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words. You may assume the dictionary does not contain duplicate words.

For example, given
s = "leetcode",
dict = ["leet", "code"].

Return true because "leetcode" can be segmented as "leet code".

UPDATE (2017/1/4):
The wordDict parameter had been changed to a list of strings (instead of a set of strings). Please reload the code definition to get the latest changes.
*/

// 自从听了老爷子的FA课以后，一直很喜欢DP问题自底向上的解法。自底向上的解法使用look数组保存已经出现的解，使用decision数组保存路径，然后套用递归即可。
// 自顶向下则需要自己把整个递归步骤预先想好，然后改写自底向上的递归，使之可以从头开始。
// 这个解法的问题就是不直观。自底向上非常直观，把大问题分解为小问题。自顶向下就很难想。
// 自底向上用好look数组与自底向下有什么区别？理论上讲，自底向上虽然容易想，但确实更消耗资源，因为这个方法多了函数递归栈。但是容易想才是王道啊！
// 说了这么多，这道题为何还用自顶向上的方法呢？
// 那是因为look数组是boolean数组，只能储存true和false，没法用第三个值来表示look的值还没有计算了！
// 倒着计算的时候你需要数组预先存满一个值来表示这个值没有计算过，这里就没法做了。其实可以改用int数组，可那也太难看了对不对。
// 所以硬着头皮，自顶向下来吧！
// 本题大致等同于FA里的切木板（WWKWW）问题。
// 最后说一句，这里look数组比l更长，是为了让0号位设置为true。这样做的目的是为了让look[j]==true那一个if判断有法可依。（否则全都是false了）
// WB(l) = WB(k-1) && wordDict.contains(s[k..l]) for all k < l
// if there is k that can make WB(l) true, then WB(l) = true; else false

class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        if (s == null || s.length() == 0) return false;
        int l = s.length();
        boolean[] look = new boolean[l+1];
        look[0] = true;
        for (int i = 1; i < l+1; i++) {
            for (int j = 0; j < i; j++) {
                String sub = s.substring(j,i);
                if (look[j] == true && wordDict.contains(sub)) {
                    look[i] = true;
                    break;
                }
            }
        }
        return look[l];
    }
}
```
