# 24 Swap Nodes in Pairs

```java
/*
Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given 1->2->3->4, you should return the list as 2->1->4->3.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.
*/

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

// 中等题。这道题不难实现，主要是需要自己画图才能看明白。关键是拿到每次交换部分的前驱节点。
// 使用多个指针。由于会换头，所以使用了哨兵。注意循环内各种指针的挂载和重连。

class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode sentinel = new ListNode(0);
        ListNode succ = null;
        ListNode prev = sentinel;
        while (head != null && head.next != null) {
            succ = head.next;
            prev.next = succ;
            head.next = succ.next;
            succ.next = head;
            prev = head;
            head = head.next;
        }
        return sentinel.next;
    }
}
```
