# 140 Word Break II

```java
/*
Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, add spaces in s to construct a sentence where each word is a valid dictionary word. You may assume the dictionary does not contain duplicate words.

Return all such possible sentences.

For example, given
s = "catsanddog",
dict = ["cat", "cats", "and", "sand", "dog"].

A solution is ["cats and dog", "cat sand dog"].

UPDATE (2017/1/4):
The wordDict parameter had been changed to a list of strings (instead of a set of strings). Please reload the code definition to get the latest changes.

*/

class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        return DFS(s, wordDict, new HashMap<String, List<String>>());
    }
    private List<String> DFS(String s, List<String> wordDict, Map<String, List<String>> map) {
        if (map.containsKey(s)) return map.get(s);
        if (s.length() == 0) return Arrays.asList("");
        List<String> list = new LinkedList<String>();
        for (String word : wordDict) {
            if (s.startsWith(word)) {
                List<String> sublist = DFS(s.substring(word.length()), wordDict, map);
                for (String sub : sublist) {
                    list.add(word + (sub.length() == 0 ? "" : " ") + sub);
                }
            }
        }
        map.put(s, list);
        return list;
    }
    /*
    public List<String> wordBreak(String s, List<String> wordDict) {
        Set<String> set = new HashSet<>();
        for (String word : wordDict) {
            set.add(word);
        }
        List<String> list = new LinkedList<>();
        DFS(s, "", set, list);
        return list;
    }
    private void DFS(String s, String str, Set<String> set, List<String> list) {
        if (set.contains(s)) {
            list.add(str + s);
        }
        for (int i = 1; i < s.length(); i++) {
            String sub = s.substring(0, i);
            if (set.contains(sub)) {
                DFS(s.substring(i), (str + sub + " "), set, list);
            }
        }
    }
    */
}
```
