# 22 Generate Parentheses

```java
/*
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
*/

class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> list = new LinkedList<>();
        StringBuilder str = new StringBuilder();
        DFS(list, str, n, n);
        return list;
    }

    private void DFS(List<String> list, StringBuilder str, int l, int r) {
        if (l == 0 && r == 0) {
            list.add(str.toString());
            return;
        }
        if (l > 0) {
            str.append('(');
            DFS(list, str, l-1, r);
            str.delete(str.length()-1, str.length());
        }
        if (l < r) {
            str.append(')');
            DFS(list, str, l, r-1);
            str.delete(str.length()-1, str.length());
        }
    }
}
```

