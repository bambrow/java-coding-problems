# 143 Reorder List

```java
/*
Given a singly linked list L: L0?L1?…?Ln-1?Ln,
reorder it to: L0?Ln?L1?Ln-1?L2?Ln-2?…

You must do this in-place without altering the nodes' values.

For example,
Given {1,2,3,4}, reorder it to {1,4,2,3}.
*/

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

// 本题实质上是链表左半部分与链表翻转后的右半部分交错合并。
// 步骤：快慢指针切分列表，翻转右半部分，交错合并。
// 翻转与交错合并分别用两个函数写成。
// 注意快慢指针拆分列表，若为偶数节点数则对半拆分；否则左半部分会比右半部分多一个节点。
// 所以合并最后一步检测是否左半部分多出来这一个节点，并且正确设置prev.next。

class Solution {
    public void reorderList(ListNode head) {
        if (head == null || head.next == null) return;
        ListNode fast = head;
        ListNode slow = head;
        while (fast.next != null && fast.next.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        fast = slow.next;
        slow.next = null;
        fast = reverse(fast);
        head = combine(head, fast);
    }

    public ListNode reverse(ListNode head) {
        ListNode prev = null;
        ListNode succ = null;
        while (head != null) {
            succ = head.next;
            head.next = prev;
            prev = head;
            head = succ;
        }
        return prev;
    }

    public ListNode combine(ListNode prev, ListNode succ) {
        ListNode head = prev;
        while (prev != null && succ != null) {
            ListNode prevNext = prev.next;
            prev.next = succ;
            ListNode succNext = succ.next;
            succ.next = prevNext;
            prev = prevNext;
            succ = succNext;
        }
        if (prev != null) prev.next = succ;
        return head;
    }
}
```
