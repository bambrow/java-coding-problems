# 47 Permutations II

```java
/*
Given a collection of numbers that might contain duplicates, return all possible unique permutations.

For example,
[1,1,2] have the following unique permutations:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
*/

// 这道题的套路是类似的。使用一个map来追踪剩余可以入选的数字。（map要提前创建好，因此要首先遍历一次数组）
// 本质上与使用boolean数组标定每个数字是否被使用过是相同的。
// 在向ans里添加cur的时候，一定要把cur复制一遍，因为cur是一个对象。

class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        List<Integer> cur = new ArrayList<>(nums.length);
        Map<Integer,Integer> map = new HashMap<>();
        for (int num : nums) {
            if (!map.containsKey(num)) map.put(num, 1);
            else map.replace(num, map.get(num)+1);
        }
        DFS(cur, nums.length, ans, map);
        return ans;
    }
    
    public void DFS(List<Integer> cur, int height, List<List<Integer>> ans, Map<Integer,Integer> map) {
        if (height == 0) {
            ans.add(new ArrayList<Integer>(cur));
            return;
        }
        for (int key : map.keySet()) {
            if (map.get(key) == 0) continue;
            map.replace(key, map.get(key)-1);
            cur.add(key);
            DFS(cur, height-1, ans, map);
            cur.remove(cur.size()-1);
            map.replace(key, map.get(key)+1);
        }
    }
}
```

