# 103 Binary Tree Zigzag Level Order Traversal

```java
/*
Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its zigzag level order traversal as:
[
  [3],
  [20,9],
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

// BFS，Z字型版
// 使用双向队列。这里用LinkedList表示。
// 使用leftSide来标记应该从左往右处理还是从右往左处理。
// 如果需要从左往右处理，那么下一层需要从右往左。首先从左侧读取节点。
// 此时将左、右child从末端加入队列。
// 如果需要从右往左处理，那么下一层需要从左往右。首先从右侧读取节点。
// 此时将右、左child从首端加入队列。
// 同样使用levelCount来标记每一层节点数。

class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> list = new LinkedList<>();
        Deque<TreeNode> deque = new LinkedList<>();
        TreeNode cur = root;
        if (cur == null) return list;
        boolean fromLeftToRight = true;
        deque.offerFirst(cur);
        while (!deque.isEmpty()) {
            int levelCount = deque.size();
            List<Integer> level = new LinkedList<>();
            for (int i = 0; i < levelCount; i++) {
                cur = fromLeftToRight ? deque.pollFirst() : deque.pollLast();
                level.add(cur.val);
                offerChildren(cur, deque, fromLeftToRight);
            }
            list.add(level);
            fromLeftToRight = !fromLeftToRight;
        }
        return list;
    }
    private void offerChildren(TreeNode cur, Deque<TreeNode> deque, boolean fromLeftToRight) {
        if (fromLeftToRight) {
            if (cur.left != null) deque.offerLast(cur.left);
            if (cur.right != null) deque.offerLast(cur.right);
        } else {
            if (cur.right != null) deque.offerFirst(cur.right);
            if (cur.left != null) deque.offerFirst(cur.left);
        }
    }
}


// 以上是重写的解法，以下是原解法。

class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {

        List<List<Integer>> res = new LinkedList<>();

        if (root != null) {

            Deque<TreeNode> deque = new LinkedList<>();
            boolean leftSide = true;
            deque.offerFirst(root);

            while (!deque.isEmpty()) {
                int levelCount = deque.size();
                List<Integer> snapshot = new LinkedList<>();
                TreeNode cur = null;
                for (int i = 0; i < levelCount; i++) {
                    if (leftSide) {
                        cur = deque.pollFirst();
                        snapshot.add(cur.val);
                        if (cur.left != null) deque.offerLast(cur.left);
                        if (cur.right != null) deque.offerLast(cur.right);
                    } else {
                        cur = deque.pollLast();
                        snapshot.add(cur.val);
                        if (cur.right != null) deque.offerFirst(cur.right);
                        if (cur.left != null) deque.offerFirst(cur.left);
                    }
                }
                res.add(snapshot);
                leftSide = !leftSide;
            }

        }

        return res;

    }
}
```

