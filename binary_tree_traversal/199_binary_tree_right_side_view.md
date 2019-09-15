# 199 Binary Tree Right Side View

```java
/*
Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

For example:
Given the following binary tree,
   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
You should return [1, 3, 4].
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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> list = new LinkedList<>();
        int[] depth = new int[2]; // depth[0] max depth for now; depth[1] current depth
        DFS(root, list, depth);
        return list;
    }
    private void DFS(TreeNode node, List<Integer> list, int[] depth) {
        TreeNode cur = node;
        if (cur == null) return;
        if (++depth[1] > depth[0]) {
            list.add(cur.val);
            depth[0]++;
        }
        DFS(cur.right, list, depth);
        DFS(cur.left, list, depth);
        depth[1]--;
    }
    /*
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> list = new LinkedList<>();
        Stack<TreeNode> stack = new Stack<>();
        int[] depth = new int[2]; // depth[0] max depth for now; depth[1] current depth
        TreeNode node = root;
        DFS(node, stack, list, depth);
        return list;
    }
    private void DFS(TreeNode node, Stack<TreeNode> stack, List<Integer> list, int[] depth) {
        if (node == null) return;
        TreeNode cur = node;
        int pushed = pushDownRight(cur, stack, list, depth);
        for (int i = 0; i < pushed; i++) {
            cur = stack.pop();
            DFS(cur.left, stack, list, depth);
            depth[1]--;
        }
    }
    private int pushDownRight(TreeNode cur, Stack<TreeNode> stack, List<Integer> list, int[] depth) {
        int pushed = 0;
        while (cur != null) {
            stack.push(cur);
            pushed++;
            if (++depth[1] > depth[0]) {
                depth[0]++;
                list.add(cur.val);
            }
            cur = cur.right;
        }
        return pushed;

    }
    */
}
```

