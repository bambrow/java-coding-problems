# 95 Unique Binary Search Trees II

```java
/*
Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1...n.

For example,
Given n = 3, your program should return all 5 unique BST's shown below.

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
*/

/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

// 这道题有点意思。是96的升级版。
// 这里的基本思路就是把所有可能的左子树根节点加入一个列表，把所有可能的右子树根节点加入另一个列表。
// 这样对于任意i，我们都有了其左子树与右子树的全排列。
// 然后我们构建i的所有可能，将左右子树嵌套遍历一遍，放在i的下面就可以了。
// 然后输出i的列表，为上一层继续做准备。

class Solution {
    public List<TreeNode> generateTrees(int n) {
        if (n == 0) return (new ArrayList<TreeNode>());
        return generateTree(1, n);
    }

    public List<TreeNode> generateTree(int start, int stop) {
        List<TreeNode> trees = new ArrayList<>();
        if (start > stop) {
            trees.add(null);
            return trees;
        }
        for (int i = start; i <= stop; i++) {
            List<TreeNode> leftSubtrees = generateTree(start, i-1);
            List<TreeNode> rightSubtrees = generateTree(i+1, stop);
            for (TreeNode leftChild : leftSubtrees) {
                for (TreeNode rightChild : rightSubtrees) {
                    TreeNode root = new TreeNode(i);
                    root.left = leftChild;
                    root.right = rightChild;
                    trees.add(root);
                }
            }
        }
        return trees;
    }
}
```

