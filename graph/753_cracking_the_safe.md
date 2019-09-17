# 753 Cracking the Safe

```java
/*
There is a box protected by a password. The password is n digits, where each letter can be one of the first k digits 0, 1, ..., k-1.

You can keep inputting the password, the password will automatically be matched against the last n digits entered.

For example, assuming the password is "345", I can open it when I type "012345", but I enter a total of 6 digits.

Please return any string of minimum length that is guaranteed to open the box after the entire string is inputted.

Example 1:
Input: n = 1, k = 2
Output: "01"
Note: "10" will be accepted too.
Example 2:
Input: n = 2, k = 2
Output: "00110"
Note: "01100", "10011", "11001" will be accepted too.
Note:
n will be in the range [1, 4].
k will be in the range [1, 10].
k^n will be at most 4096.
*/

class Solution {
    public String crackSafe(int n, int k) {
        StringBuilder str = new StringBuilder();
        int goal = (int) (Math.pow(k, n));
        for (int i = 0; i < n; i++) {
            str.append(0);
        }
        Set<String> set = new HashSet<>();
        set.add(str.toString());
        DFS(str, goal, set, n, k);
        return str.toString();
    }

    private boolean DFS(StringBuilder str, int goal, Set<String> set, int n, int k) {
        if (set.size() == goal) return true;
        String prev = str.substring(str.length() - n + 1, str.length());
        for (int i = 0; i < k; i++) {
            String next = prev + i;
            if (!set.contains(next)) {
                set.add(next);
                str.append(i);
                if (DFS(str, goal, set, n, k)) {
                    return true;
                } else {
                    set.remove(next);
                    str.delete(str.length() - 1, str.length());
                }
            }
        }
        return false;
    }
}
```
