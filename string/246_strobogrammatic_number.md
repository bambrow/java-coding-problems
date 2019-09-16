# 246 Strobogrammatic Number

```java
/*
A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Write a function to determine if a number is strobogrammatic. The number is represented as a string.

For example, the numbers "69", "88", and "818" are all strobogrammatic.

*/

class Solution {
    public boolean isStrobogrammatic(String num) {
        int i = 0, j = num.length()-1;
        while (i <= j) {
            char p = num.charAt(i), q = num.charAt(j);
            if (p != '0' && p != '1' && p != '6' && p != '8' && p != '9') return false;
            if ((p == '6' && q != '9') || (p == '9' && q != '6')) return false;
            if ((p == '0' || p == '1' || p == '8') && (p != q)) return false;
            i++;
            j--;
        }
        return true;
    }
}
```
