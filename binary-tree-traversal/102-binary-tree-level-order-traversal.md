# 102 Binary Tree Level Order Traversal

```java
/*
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its level order traversal as:
[
  [3],
  [9,20],
  [15,7]
]
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

// BFS
// 需要使用队列。这里用LinkedList表示队列。
// 首先处理当前节点（新出列），然后将它所有children加入队列。
// 这里使用levelCount来保存了每一层的节点数。

class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> list = new LinkedList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        TreeNode cur = root;
        if (cur == null) return list;
        queue.offer(cur);
        while (!queue.isEmpty()) {
            int levelCount = queue.size();
            List<Integer> level = new LinkedList<>();
            for (int i = 0; i < levelCount; i++) {
                cur = queue.poll();
                level.add(cur.val);
                offerChildren(cur, queue);
            }
            list.add(level);
        }
        return list;
    }
    private void offerChildren(TreeNode cur, Queue<TreeNode> queue) {
        if (cur.left != null) queue.offer(cur.left);
        if (cur.right != null) queue.offer(cur.right);
    }
}


// 以上是重写的解法，以下是原解法。

class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        
        List<List<Integer>> res = new LinkedList<>();
        
        if (root != null) {
            
            Queue<TreeNode> queue = new LinkedList<>();
            queue.offer(root);
            
            while (!queue.isEmpty()) {
                int levelCount = queue.size();
                List<Integer> snapshot = new LinkedList<>();
                TreeNode cur = null;
                for (int i = 0; i < levelCount; i++) {
                    cur = queue.poll();
                    snapshot.add(cur.val);
                    if (cur.left != null) queue.offer(cur.left);
                    if (cur.right != null) queue.offer(cur.right);
                }
                res.add(snapshot);
            }
            
        }
        
        return res;
        
    }
}
```

