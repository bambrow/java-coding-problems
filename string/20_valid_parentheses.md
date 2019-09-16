# 20 Valid Parentheses

```java
/*
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.
*/

class Solution {
    public boolean isValid(String s) {

        Stack<Character> stack = new Stack<>();
        String left = "([{";
        String right = ")]}";
        for (char c : s.toCharArray()) {
            if (left.indexOf(c) != -1) stack.push(c);
            else if (right.indexOf(c) != -1) {
                if (stack.isEmpty()) return false;
                if (right.indexOf(c) != left.indexOf(stack.pop())) return false;
            }
        }
        return stack.isEmpty();

    }
}
```
