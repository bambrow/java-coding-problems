# 78 Subsets

```java
/*
Given a set of distinct integers, nums, return all possible subsets.

Note: The solution set must not contain duplicate subsets.

For example,
If nums = [1,2,3], a solution is:

[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
*/

// 感觉这才是回溯的入门题。这道题难度低于17/39/40/77，可以说是非常友好了。思路几乎完全相同，不赘述了。

class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        List<Integer> cur = new ArrayList<>();
        DFS(nums, 0, ans, cur);
        return ans;
    }
    
    public void DFS(int[] nums, int level, List<List<Integer>> ans, List<Integer> cur) {
        ans.add(new ArrayList<Integer>(cur));
        if (level == nums.length) return;
        for (int i = level; i < nums.length; i++) {
            cur.add(nums[i]);
            DFS(nums, i+1, ans, cur);
            cur.remove(cur.size()-1);
        }
    }
}
```

