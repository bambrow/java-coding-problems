# 118 Pascal's Triangle

```java
/*
Given numRows, generate the first numRows of Pascal's triangle.

For example, given numRows = 5,
Return

[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
*/

// 本解法重复利用row列表。每次在列表前端插入一个1，然后从1下标开始计算新值。
// row.set(j, row.get(j)+row.get(j+1)); 这句最关键。
// 新的j下标所存储的数据应该是原来的j-1与j下标的数据之和，但因为开始新插入了1，所以变成了j与j+1之和。
// 注意ans每一层加入的是row的copy，不能直接添加row。

class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> ans = new ArrayList<>();
        List<Integer> row = new ArrayList<>();
        for (int i = 0; i < numRows; i++) {
            row.add(0, 1);
            for (int j = 1; j < row.size()-1; j++) {
                row.set(j, row.get(j)+row.get(j+1));
            }
            ans.add(new ArrayList<Integer>(row));
        }
        return ans;
    }
}
```
