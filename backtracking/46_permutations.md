# 46 Permutations

```java
/*
Given a collection of distinct numbers, return all possible permutations.

For example,
[1,2,3] have the following permutations:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
*/

// 还是原来的配方，还是熟悉的味道。这道题采用了算法课本中的解法，并尽量保持与其他回溯题目风格一致。这里其实使用level不是特别好理解，我们还可以修改一下形式。

class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        DFS(nums, 0, ans);
        return ans;
    }

    public void DFS(int[] nums, int level, List<List<Integer>> ans) {
        if (level == nums.length) {
            ans.add(generateList(nums));
            return;
        }
        for (int i = nums.length-1; i >= level; i--) {
            int temp = nums[i]; nums[i] = nums[level]; nums[level] = temp;
            DFS(nums, level+1, ans);
            temp = nums[i]; nums[i] = nums[level]; nums[level] = temp;
        }
    }

    public List<Integer> generateList(int[] nums) {
        List<Integer> list = new ArrayList<>(nums.length);
        for (int num: nums) list.add(num);
        return list;
    }
}

// 这里采用height代替了level，代码更容易理解。原理就是通过互换元素以达到所有可能排列的效果。
// 如果后n-1个元素固定，只有第一个元素，那么很显然已经不用互换，可以增加一个结果；
// 如果后n-2个元素固定，只有前两个元素，那么会有两元素互换与两元素不互换（这种情况下其实是第二个元素与自己互换了，相当于没有变化），达成所有可能。
// 同理，当后n-k个元素固定时，只有前k个元素，那么依旧可以达成所有可能。
// 所以对于前n个元素（即所有元素），该方法亦保证了一切可能。

class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        DFS(nums, nums.length-1, ans);
        return ans;
    }

    public void DFS(int[] nums, int height, List<List<Integer>> ans) {
        if (height == 0) {
            ans.add(generateList(nums));
            return;
        }
        for (int i = 0; i <= height; i++) {
            int temp = nums[i]; nums[i] = nums[height]; nums[height] = temp;
            DFS(nums, height-1, ans);
            temp = nums[i]; nums[i] = nums[height]; nums[height] = temp;
        }
    }

    public List<Integer> generateList(int[] nums) {
        List<Integer> list = new ArrayList<>(nums.length);
        for (int num: nums) list.add(num);
        return list;
    }
}

```

