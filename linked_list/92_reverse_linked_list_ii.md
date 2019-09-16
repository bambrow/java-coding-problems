# 92 Reverse Linked List II

```java
/*
Reverse a linked list from position m to n. Do it in-place and in one-pass.

For example:
Given 1->2->3->4->5->NULL, m = 2 and n = 4,

return 1->4->3->2->5->NULL.

Note:
Given m, n satisfy the following condition:
1 ≤ m ≤ n ≤ length of list.
*/

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

// 可能要换头，所以设置哨兵。其余的需要画图理解，详见代码。

class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if (head == null) return head;
        ListNode sentinel = new ListNode(0);
        sentinel.next = head;
        ListNode prev = sentinel;
        for (int i = 1; i < m; i++) prev = prev.next;
        ListNode cur = prev.next;
        for (int i = m; i < n; i++) {
            ListNode succ = cur.next;
            cur.next = succ.next;
            succ.next = prev.next;
            prev.next = succ;
        }
        return sentinel.next;
    }
}
```
