# 19 Remove Nth Node From End of List

```java
/*
Given a linked list, remove the nth node from the end of list and return its head.

For example,

   Given linked list: 1->2->3->4->5, and n = 2.

   After removing the second node from the end, the linked list becomes 1->2->3->5.
Note:
Given n will always be valid.
Try to do this in one pass.
*/

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

// 这里保证n是有效的。我们先遍历链表，每次都让n减1，直到n为0为止。
// 然后建立一个哨兵，并且让prev指向哨兵。接下来cur与prev一起走直到cur为null为止。
// 此时prev所在的位置是要删除的节点的前一个位置。
// 因为可能会删除头节点，所以哨兵是必要的。

class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null) return head;
        ListNode cur = head;
        while (n > 0) {
            n--;
            cur = cur.next;
        }
        ListNode sentinel = new ListNode(0);
        sentinel.next = head;
        ListNode prev = sentinel;
        while (cur != null) {
            cur = cur.next;
            prev = prev.next;
        }
        prev.next = prev.next.next;
        return sentinel.next;
    }
}

// 上题是假设n有效。如果n不一定有效，可以采用下面的代码：
// 首先遍历一遍列表，同时让n不断减少，来探测n是否有效。如果最后n大于0，那么根本不存在倒数第n个节点。
// n=0，则要删除的是头节点。
// n<0，就重新开始遍历，不停让n相加，直到n为0（注意是先相加再检查），此时所在的节点是要删除的节点前面的节点。
// 最后返回头节点。

class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null || n < 0) return head;
        ListNode cur = head;
        while (cur != null) {
            n--;
            cur = cur.next;
        }
        if (n == 0) head = head.next;
        if (n < 0) {
            cur = head;
            while (++n != 0) cur = cur.next;
            cur.next = cur.next.next;
        }
        return head;
    }
}

```
