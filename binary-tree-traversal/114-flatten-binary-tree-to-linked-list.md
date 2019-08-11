# 114 Flatten Binary Tree to Linked List

```java
/*
Given a binary tree, flatten it to a linked list in-place.

For example,
Given

         1
        / \
       2   5
      / \   \
     3   4   6
The flattened tree should look like:
   1
    \
     2
      \
       3
        \
         4
          \
           5
            \
             6
click to show hints.

Hints:
If you notice carefully in the flattened tree, each node's right child points to the next node of a pre-order traversal.
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

// 首先找到cur左子树的最右节点。记为pre。
// pre右侧指向cur的右侧。
// cur的右侧指向cur的左侧。清空cur的左侧。
// 此时cur的右侧是本来cur左侧的内容。令cur等于cur的右child，继续处理。
// 本题还有一种思路，处理之后的节点其实就是preorder的顺序。可以选择做preorder遍历，同时处理指针。

class Solution {
    public void flatten(TreeNode root) {
        if (root == null) return;
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        TreeNode prev = new TreeNode(0);
        stack.push(cur);
        while (!stack.isEmpty()) {
            cur = stack.pop();
            prev.left = null;
            prev.right = cur;
            prev = prev.right;
            pushChildren(cur, stack);
        }
    }
    private void pushChildren(TreeNode cur, Stack<TreeNode> stack) {
        if (cur.right != null) stack.push(cur.right);
        if (cur.left != null) stack.push(cur.left);
    }
}


// 以上是容易理解的preorder思路。

class Solution {
    public void flatten(TreeNode root) {
        
        if (root == null) return;
        TreeNode cur = root;
        while (cur != null) {
            if (cur.left != null) {
                TreeNode pre = cur.left;
                while (pre.right != null) pre = pre.right;
                pre.right = cur.right;
                cur.right = cur.left;
                cur.left = null;
            }
            cur = cur.right;
        }
        
    }
}
```

