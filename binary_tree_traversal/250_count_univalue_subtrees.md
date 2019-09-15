# 250 Count Univalue Subtrees

```java
/*
Given a binary tree, count the number of uni-value subtrees.

A Uni-value subtree means all nodes of the subtree have the same value.

For example:
Given binary tree,
              5
             / \
            1   5
           / \   \
          5   5   5
return 4.
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
    private int num = 0;
    public int countUnivalSubtrees(TreeNode root) {
        if (root == null) return 0;
        testSubtree(root, root.val);
        return num;
    }
    private boolean testSubtree(TreeNode node, int val) {
        if (node == null) return true;
        if (node.val != val) {
            testSubtree(node, node.val);
            return false;
        } else {
            boolean l = testSubtree(node.left, val);
            boolean r = testSubtree(node.right, val);
            if (l && r) {
                num++;
                return true;
            }
        }
        return false;
    }
}
```

