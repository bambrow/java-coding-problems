# 144 Binary Tree Preorder Traversal

```java
/*
Given a binary tree, return the preorder traversal of its nodes' values.

For example:
Given binary tree {1,#,2,3},
   1
    \
     2
    /
   3
return [1,2,3].

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

// preorder
// 使用stack。首先压入根节点。然后弹出栈顶节点，进行处理，然后分别压入右、左child节点（如有）。
// 先压入右，再压入左，可以保证处理时先左后右。
// 这样可保证为中-左-右顺序。

class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> list = new LinkedList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        if (cur == null) return list;
        stack.push(cur);
        while (!stack.isEmpty()) {
            cur = stack.pop();
            list.add(cur.val);
            pushChildren(cur, stack);
        }
        return list;
    }
    private void pushChildren(TreeNode cur, Stack<TreeNode> stack) {
        if (cur.right != null) stack.push(cur.right);
        if (cur.left != null) stack.push(cur.left);
    }
}


// 以上是重写的解法，以下是原解法。

class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {

        List<Integer> res = new LinkedList<>();

        if (root != null) {
            Stack<TreeNode> stack = new Stack<TreeNode>();
            stack.push(root);
            TreeNode cur = null;
            while (!stack.isEmpty()) {
                cur = stack.pop();
                res.add(cur.val);
                if (cur.right != null) stack.push(cur.right);
                if (cur.left != null) stack.push(cur.left);
            }
        }

        return res;

    }
}
```

