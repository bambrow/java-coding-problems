# 106 Construct Binary Tree from Inorder and Postorder Traversal

```java
/*
Given inorder and postorder traversal of a tree, construct the binary tree.

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

// 处理方式与105类似，只是postorder数组需要倒序遍历，并且先处理右侧节点再处理左侧。

class Solution {
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        
        if (inorder.length == 0 || postorder.length == 0) return null;
        
        TreeNode root = new TreeNode(postorder[postorder.length - 1]);
        TreeNode cur = root;
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        boolean rightSide = true;
        
        for (int i=postorder.length-2, j=postorder.length-1; i >= 0; ) {
            if (!stack.isEmpty() && stack.peek().val == inorder[j]) {
                cur = stack.pop();
                rightSide = false;
                j--;
            } else if (rightSide) {
                cur.right = new TreeNode(postorder[i]);
                cur = cur.right;
                stack.push(cur);
                i--;
            } else {
                cur.left = new TreeNode(postorder[i]);
                cur = cur.left;
                stack.push(cur);
                rightSide = true;
                i--;
            }
        }
        
        return root;
        
    }
}
```

