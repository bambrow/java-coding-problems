# 530 Minimum Absolute Difference in BST

```java
/*
Given a binary search tree with non-negative values, find the minimum absolute difference between values of any two nodes.

Example:

Input:

   1
    \
     3
    /
   2

Output:
1

Explanation:
The minimum absolute difference is 1, which is the difference between 2 and 1 (or between 2 and 3).
Note: There are at least two nodes in this BST.
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
class Solution {

    public int getMinimumDifference(TreeNode root) {
        int min = Integer.MAX_VALUE;
        int prev = (root.left != null) ? root.val : root.right.val;
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        while (!stack.isEmpty() || cur != null) {
            if (cur != null) {
                stack.push(cur);
                cur = cur.left;
            } else {
                cur = stack.pop();
                min = Math.min(min, Math.abs(cur.val-prev));
                prev = cur.val;
                cur = cur.right;
            }
        }
        return min;
    }

    /*
    public int getMinimumDifference(TreeNode root) {
        int min = Integer.MAX_VALUE;
        if (root.left != null) {
            TreeNode pred = root.left;
            while (pred.right != null) pred = pred.right;
            int diff = Math.abs(root.val - pred.val);
            diff = Math.min(diff, getMinimumDifference(root.left));
            min = Math.min(min, diff);
        }
        if (root.right != null) {
            TreeNode succ = root.right;
            while (succ.left != null) succ = succ.left;
            int diff = Math.abs(root.val - succ.val);
            diff = Math.min(diff, getMinimumDifference(root.right));
            min = Math.min(min, diff);
        }
        return min;
    }
    */
}
```
