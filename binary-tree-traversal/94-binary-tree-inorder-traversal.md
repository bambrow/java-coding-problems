# 94 Binary Tree Inorder Traversal

```java
/*
Given a binary tree, return the inorder traversal of its nodes' values.

For example:
Given binary tree [1,null,2,3],
   1
    \
     2
    /
   3
return [1,3,2].

Note: Recursive solution is trivial, could you do it iteratively?
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

// inorder
// 使用stack。原则：如果可能，尝试push左边的child；如果为null，pop一个节点，处理后尝试push右边的child
// 如是进行下去可以保证为左-中-右的遍历顺序。

class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new LinkedList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        pushDownLeft(cur, stack);
        while (!stack.isEmpty()) {
            cur = stack.pop();
            list.add(cur.val);
            pushDownLeft(cur.right, stack);
        }
        return list;
    }
    private void pushDownLeft(TreeNode cur, Stack<TreeNode> stack) {
        while (cur != null) {
            stack.push(cur);
            cur = cur.left;
        }
    }
}


// 原解法，代码类似，只是上面的代码更简洁。

class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {

        List<Integer> res = new LinkedList<>();

        if (root != null) {
            Stack<TreeNode> stack = new Stack<>();
            TreeNode cur = root;
            while (!stack.isEmpty() || cur != null) {
                if (cur != null) {
                    stack.push(cur);
                    cur = cur.left;
                } else {
                    cur = stack.pop();
                    res.add(cur.val);
                    cur = cur.right;
                }
            }
        }

        return res;
    }
}
```

