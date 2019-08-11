# 255 Verify Preorder Sequence in Binary Search Tree

```java
/*
Given an array of numbers, verify whether it is the correct preorder traversal sequence of a binary search tree.

You may assume each number in the sequence is unique.

Follow up:
Could you do it using only constant space complexity?
*/

class Solution {
    public boolean verifyPreorder(int[] preorder) {
        int small = Integer.MIN_VALUE;
        int i = -1;
        for (int num : preorder) {
            if (num < small) return false;
            while (i >= 0 && num > preorder[i]) small = preorder[i--];
            preorder[++i] = num;
        }
        return true;
    }
    /*
    public boolean verifyPreorder(int[] preorder) {
        int small = Integer.MIN_VALUE;
        Stack<Integer> stack = new Stack<>();
        for (int num : preorder) {
            if (num < small) return false;
            while (!stack.isEmpty() && num > stack.peek()) small = stack.pop();
            stack.push(num);
        }
        return true;
    }
    */
}
```

