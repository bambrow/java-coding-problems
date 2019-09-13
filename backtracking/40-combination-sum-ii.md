# 40 Combination Sum II

```java
/*
Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

Each number in C may only be used once in the combination.

Note:
All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.
For example, given candidate set [10, 1, 2, 7, 6, 1, 5] and target 8,
A solution set is:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
*/

// 类似39。改动的点是数字不允许重复使用（但出现k次的数字最多可以使用k次），并且不允许出现重复的组合。
// 前一个改动可以通过在DFS递归的时候使下一层为i+1来实现。
// 后一个改动通过for循环里最后一行while来实现。其目的是略过之后的重复数字。对于示例来讲，排序好的数组为[1,1,2,5,6,7,10]，这行代码避免了第一个1做完递归之后再用第二个1重来了一遍递归，给出重复的结果。
// 当然，要实现后一个改动，数组要事先排序。

class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        if (target <= 0 || candidates.length == 0) return ans;
        Arrays.sort(candidates);
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
            DFS(candidates, target, i+1, ans, cur);
            target += candidates[i];
            cur.remove(cur.size()-1);
            while(i < candidates.length-1 && candidates[i] == candidates[i+1]) i++;
        }
    }
}
```

