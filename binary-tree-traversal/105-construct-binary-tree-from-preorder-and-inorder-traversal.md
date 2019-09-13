# 105 Construct Binary Tree from Preorder and Inorder Traversal

```java
/*
Given preorder and inorder traversal of a tree, construct the binary tree.

Note:
You may assume that duplicates do not exist in the tree.
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

// 从preorder和inorder中建立树。
// preorder的首个节点是根节点，先压入栈。
// 从preorder的第1位置和inorder的第0位置开始遍历。
// 如果栈不为空并且栈顶元素与inorder当前元素相等，证明左子树已经处理完毕（或为空）。此时标记为可以处理右侧节点，然后弹出当前节点。
// 否则，看是否需要处理左子树，如果可能的话一直向左处理（表现为仅遍历preorder）并压入处理节点。
// 如果左子树不需要处理，则处理右边第一个节点（表现为读取preorder下一个节点）并压入处理节点，重新标记为需要处理左子树。

class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {

        if (preorder.length == 0 || inorder.length == 0) return null;

        TreeNode root = new TreeNode(preorder[0]);
        TreeNode cur = root;
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        boolean leftSide = true;

        for (int i = 1, j = 0; i < preorder.length; ) {
            if (!stack.isEmpty() && stack.peek().val == inorder[j]) {
                cur = stack.pop();
                leftSide = false;
                j++;
            } else if (leftSide) {
                cur.left = new TreeNode(preorder[i]);
                cur = cur.left;
                stack.push(cur);
                i++;
            } else {
                cur.right = new TreeNode(preorder[i]);
                cur = cur.right;
                stack.push(cur);
                leftSide = true;
                i++;
            }
        }

        return root;

    }
}
```

