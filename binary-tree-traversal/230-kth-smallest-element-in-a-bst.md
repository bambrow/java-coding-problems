# 230 Kth Smallest Element in a BST

```java
/*
Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

Note:
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

Follow up:
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?
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
    private int count = 0;
    public int kthSmallest(TreeNode root, int k) {
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        pushDownLeft(cur, stack);
        while (!stack.isEmpty()) {
            cur = stack.pop();
            if (++count == k) return cur.val;
            pushDownLeft(cur.right, stack);
        }
        return -1;
    }
    private void pushDownLeft(TreeNode cur, Stack<TreeNode> stack) {
        while (cur != null) {
            stack.push(cur);
            cur = cur.left;
        }
    }
}
```

