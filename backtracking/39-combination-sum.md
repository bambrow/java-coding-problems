# 39 Combination Sum

```java
/*
Given a set of candidate numbers (C) (without duplicates) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

The same repeated number may be chosen from C unlimited number of times.

Note:
All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.
For example, given candidate set [2, 3, 6, 7] and target 7,
A solution set is:
[
  [7],
  [2, 2, 3]
]
*/

// 类似77。注意两点：level初始值从0开始（数组第一下标是0）；DFS递归代入的level是i而不是i+1，因为可以重复使用数字。

class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        if (target <= 0 || candidates.length == 0) return ans;
        List<Integer> cur = new ArrayList<>();
        DFS(candidates, target, 0, ans, cur);
        return ans;
    }

    public void DFS(int[] candidates, int target, int level, List<List<Integer>> ans, List<Integer> cur) {
        if (target == 0) {
            ans.add(new ArrayList<Integer>(cur));
            return;
        }
        if (target < 0) return;
        for (int i = level; i < candidates.length; i++) {
            cur.add(candidates[i]);
            target -= candidates[i];
            DFS(candidates, target, i, ans, cur);
            target += candidates[i];
            cur.remove(cur.size()-1);
        }
    }
}
```

