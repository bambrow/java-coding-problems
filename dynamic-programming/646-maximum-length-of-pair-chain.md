# 646 Maximum Length of Pair Chain

```java
/*
You are given n pairs of numbers. In every pair, the first number is always smaller than the second number.

Now, we define a pair (c, d) can follow another pair (a, b) if and only if b < c. Chain of pairs can be formed in this fashion.

Given a set of pairs, find the length longest chain which can be formed. You needn't use up all the given pairs. You can select pairs in any order.

Example 1:
Input: [[1,2], [2,3], [3,4]]
Output: 2
Explanation: The longest chain is [1,2] -> [3,4]
Note:
The number of given pairs will be in the range [1, 1000].
*/

// 首先对所有pairs排序。这里使用了lambda表达式作为Comparator。
// LC(0) = 1
// LC(i) = max { LC(j)+1 or LC(j) } for all 0 <= j < i,
//         choose LC(j)+1 if pair i can be chained after pair j
//         choose LC(j) if pair i cannot be chained after pair j


class Solution {
    public int findLongestChain(int[][] pairs) {
        if (pairs.length == 0 || pairs[0].length == 0) return 0;
        int l = pairs.length;
        Arrays.sort(pairs, (a,b) -> (a[0] - b[0]));
        int[] look = new int[l];
        Arrays.fill(look, 1);
        for (int i = 0; i < l; i++) {
            for (int j = 0; j < i; j++) {
                look[i] = Math.max(look[i], pairs[i][0] > pairs[j][1] ? look[j]+1 : look[j]);
            }
        }
        return look[l-1];
    }
}

```

