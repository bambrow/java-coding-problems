# 107 Binary Tree Level Order Traversal II

```java
/*
Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its bottom-up level order traversal as:
[
  [15,7],
  [9,20],
  [3]
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
// 本题与102相当类似，区别就是每一层的节点值插入到结果头部。这样可以保证是倒序。

class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> list = new ArrayList<>();
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
        for (int i = 0; i < list.size()/2; i++) {
            List<Integer> temp = list.get(i);
            int j = list.size()-i-1;
            list.set(i, list.get(j));
            list.set(j, temp);
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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        
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
                ((LinkedList) res).addFirst(snapshot);
            }
            
        }
        
        return res;
        
    }
}
```

