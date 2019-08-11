# 145 Binary Tree Postorder Traversal

```java
/*
Given a binary tree, return the postorder traversal of its nodes' values.

For example:
Given binary tree {1,#,2,3},
   1
    \
     2
    /
   3
return [3,2,1].

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

// postorder
// 依旧使用stack。这里利用了LinkedList可以向头部插入数值的特性。
// 相当于倒着插入中-右-左（stack先push了左再push了右，处理顺序相反）
// 也就是正向的左-右-中。

class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        if (cur == null) return list;
        stack.push(cur);
        while (!stack.isEmpty()) {
            cur = stack.pop();
            list.add(cur.val);
            pushChildren(cur, stack);
        }
        for (int i = 0; i < list.size()/2; i++) {
            int temp = list.get(i);
            int j = list.size()-i-1;
            list.set(i, list.get(j));
            list.set(j, temp);
        }
        return list;
    }
    private void pushChildren(TreeNode cur, Stack<TreeNode> stack) {
        if (cur.left != null) stack.push(cur.left);
        if (cur.right != null) stack.push(cur.right);
    }
}


// 以上是重写的解法，以下是原解法。

class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        
        List<Integer> res = new LinkedList<>();
        
        if (root != null) {
            Stack<TreeNode> stack = new Stack<>();
            stack.push(root);
            TreeNode cur = null;
            while (!stack.isEmpty()) {
                cur = stack.pop();
                ((LinkedList) res).addFirst(cur.val);
                if (cur.left != null) stack.push(cur.left);
                if (cur.right != null) stack.push(cur.right);
            }
        }
        
        return res;
        
    }
}
```

