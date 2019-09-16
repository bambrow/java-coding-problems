# 270 Closest Binary Search Tree Value

```java
/*
Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

Note:
Given target value is a floating point.
You are guaranteed to have only one unique value in the BST that is closest to the target.
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
    public int closestValue(TreeNode root, double target) {
        int val = root.val;
        double diff = Math.abs(val-target);
        TreeNode cur = root;
        while (cur != null) {
            if (Math.abs(cur.val-target) < diff) {
                val = cur.val;
                diff = Math.abs(cur.val-target);
            }
            if (target > cur.val) cur = cur.right;
            else cur = cur.left;
        }
        return val;
    }
}
```
