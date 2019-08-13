# 77 Combinations

```java
/*
Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

For example,
If n = 4 and k = 2, a solution is:

[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
*/

// 本题就是求所有的组合，共有C(n,k)个。
// 递归求解，使用DFS。维持level变量来避免重复，保证后选的数大于前选的数。
// 本题思路类似于113/129/257，都是要做一个「事后还原」的步骤。

class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> ans = new ArrayList<>();
        if (n <= 0) return ans;
        List<Integer> cur = new ArrayList<>();
        DFS(n, k, 1, ans, cur);
        return ans;
    }
    
    public void DFS(int n, int k, int level, List<List<Integer>> ans, List<Integer> cur) {
        if (cur.size() == k) {
            ans.add(new ArrayList<Integer>(cur));
            return;
        }
        for (int i = level; i <= n; i++) {
            cur.add(i);
            DFS(n, k, i+1, ans, cur);
            cur.remove(cur.size()-1);
        }
    }
}
```

