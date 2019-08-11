# 285 Inorder Successor in BST

```java
/*
Given a binary search tree and a node in it, find the in-order successor of that node in the BST.

Note: If the given node has no in-order successor in the tree, return null.

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
    
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if (root == null) return null;
        TreeNode cur = root;
        TreeNode prev = null;
        while (cur.val != p.val) {
            if (cur.val > p.val) {
                prev = cur;
                cur = cur.left;
            } else if (cur.val < p.val) {
                cur = cur.right;
            }
        }
        if (cur.right != null) {
            cur = cur.right;
            while (cur != null && cur.left != null) cur = cur.left;
            return cur;
        }
        return prev;
    }
    
    /*
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if (root == null) return null;
        if (root.val <= p.val) return inorderSuccessor(root.right, p);
        else {
            TreeNode left = inorderSuccessor(root.left, p);
            return left == null ? root : left;
        }
    }
    */
}
```

