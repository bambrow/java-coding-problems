# 90 Subsets II

```java
/*
Given a collection of integers that might contain duplicates, nums, return all possible subsets.

Note: The solution set must not contain duplicate subsets.

For example,
If nums = [1,2,2], a solution is:

[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
*/

// 这道题与78的关系就是40与39的关系，多了重复元素而已。
// 做了39/40之后再来做78/90，心里还是有一丝无奈的。有种「我还没出力，你就倒下了」的感觉。

class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        List<Integer> cur = new ArrayList<>();
        Arrays.sort(nums);
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
            while (i < nums.length-1 && nums[i] == nums[i+1]) i++;
        }
    }
}
```

