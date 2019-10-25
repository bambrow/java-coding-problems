# 119 Pascal's Triangle II

```java
/*
Given an index k, return the kth row of the Pascal's triangle.

For example, given k = 3,
Return [1,3,3,1].

Note:
Could you optimize your algorithm to use only O(k) extra space?
*/

// 与118类似。解法几乎一样。
// 有个坑是119对行数的定义与118不同，所以for循环条件改成了小于等于。

class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> row = new ArrayList<>();
        for (int i = 0; i <= rowIndex; i++) {
            row.add(0, 1);
            for (int j = 1; j < row.size()-1; j++) {
                row.set(j, row.get(j)+row.get(j+1));
            }
        }
        return row;
    }
}
```
