# 25 Reverse Nodes in k-Group

```java
/*
Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

You may not alter the values in the nodes, only nodes itself may be changed.

Only constant memory is allowed.

For example,
Given this linked list: 1->2->3->4->5

For k = 2, you should return: 2->1->4->3->5

For k = 3, you should return: 3->2->1->4->5
*/

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

// 困难题。链表翻转的函数与206结构类似，只是这里采用了翻转部分的前驱节点与后继节点作为输入，并输出翻转后该区域的最后一个节点以作为下一次翻转的前驱节点。
// 主函数首先保存下一段翻转的前驱节点（就是当前的cur），然后cur向前走k步，同时判断是否剩余的节点不足k个，如果不足则不翻转最后这一部分。
// 如果足够，则将翻转部分的前驱与后继节点传入翻转函数，进行翻转，并注意用cur接收为翻转后该部分的最后一个节点，以作为下一次翻转的前驱节点（下一次循环开始cur会保存在prev中）。
// 由于会换头，这里使用了哨兵。

class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null || k <= 1) return head;
        ListNode sentinel = new ListNode(0);
        sentinel.next = head;
        ListNode prev = sentinel;
        ListNode cur = sentinel;
        while (cur != null) {
            prev = cur;
            for (int i = 0; i < k; i++) {
                cur = cur.next;
                if (cur == null) return sentinel.next;
            }
            cur = reverse(prev, cur.next);
        }
        return sentinel.next;
    }

    public ListNode reverse(ListNode prev, ListNode end) {
        ListNode head = prev.next;
        while (head.next != end) {
            ListNode succ = head.next;
            head.next = succ.next;
            succ.next = prev.next;
            prev.next = succ;
        }
        return head;
    }
}
```
