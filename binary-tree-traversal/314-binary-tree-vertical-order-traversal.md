# 314 Binary Tree Vertical Order Traversal

```java
/*
Given a binary tree, return the vertical order traversal of its nodes' values. (ie, from top to bottom, column by column).

If two nodes are in the same row and column, the order should be from left to right.

Examples:

Given binary tree [3,9,20,null,null,15,7],
   3
  /\
 /  \
 9  20
    /\
   /  \
  15   7
return its vertical order traversal as:
[
  [9],
  [3,15],
  [20],
  [7]
]
Given binary tree [3,9,8,4,0,1,7],
     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
return its vertical order traversal as:
[
  [4],
  [9],
  [3,0,1],
  [8],
  [7]
]
Given binary tree [3,9,8,4,0,1,7,null,null,null,2,5] (0's right child is 2 and 1's left child is 5),
     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
    /\
   /  \
   5   2
return its vertical order traversal as:
[
  [4],
  [9,5],
  [3,0,1],
  [8,2],
  [7]
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
class Solution {
    
    public List<List<Integer>> verticalOrder(TreeNode root) {
        
        List<List<Integer>> list = new LinkedList<>();
        if (root == null) return list;
        
        TreeNode cur = root;
        int col = 0;
        
        Map<Integer,List<Integer>> map = new HashMap<>();
        int[] range = new int[2];
        
        Queue<TreeNode> nodeQueue = new LinkedList<>();
        Queue<Integer> colQueue = new LinkedList<>();
        nodeQueue.offer(cur);
        colQueue.offer(0);
        
        while (!nodeQueue.isEmpty()) {
            int size = nodeQueue.size();
            for (int i = 0; i < size; i++) {
                cur = nodeQueue.poll();
                col = colQueue.poll();
                range[0] = Math.min(col, range[0]);
                range[1] = Math.max(col, range[1]);
                if (!map.containsKey(col)) {
                    List<Integer> colList = new LinkedList<>();
                    colList.add(cur.val);
                    map.put(col, colList);
                } else {
                    map.get(col).add(cur.val);
                }
                if (cur.left != null) {
                    nodeQueue.offer(cur.left);
                    colQueue.offer(col-1);
                }
                if (cur.right != null) {
                    nodeQueue.offer(cur.right);
                    colQueue.offer(col+1);
                }
            }
        }
        
        for (int i = range[0]; i <= range[1]; i++) {
            list.add(map.get(i));
        }
        
        return list;
        
    }
    
}

```

