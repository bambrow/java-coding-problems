# 61 Rotate List

```java
/*
Given a list, rotate the list to the right by k places, where k is non-negative.

For example:
Given 1->2->3->4->5->NULL and k = 2,
return 4->5->1->2->3->NULL.
*/

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

// 首先求链表长度，如果k大于长度n，那么取余数，然后让n=n-k%n，即需要隔断处前面的节点数。
// 巧妙的做法是将链表成环，继续走n=n-k%n个节点，所在的位置正好就是需断开的前一个节点。
// 此时直接断开链表，返回新头即可。

class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || k == 0) return head;
        ListNode cur = head;
        int n = 1;
        while (cur.next != null) {
            n++;
            cur = cur.next;
        }
        n = n - k % n;
        cur.next = head;
        for (int i = 0; i < n; i++) {
            cur = cur.next;
        }
        head = cur.next;
        cur.next = null;
        return head;
    }
}
```
