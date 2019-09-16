# 21 Merge Two Sorted Lists

```java
/*
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.
*/

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

// 简单题。注意由于我们不知道头节点是哪个，所以建立一个哨兵。然后不断比较两个链表，哪个较小，就挂载。
// 最后还要处理一下链表中未挂载的节点，因为此时两个链表中会有一个为空，另一个不为空。

class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        ListNode head = new ListNode(0);
        ListNode sentinel = head;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                head.next = l1;
                l1 = l1.next;
            } else {
                head.next = l2;
                l2 = l2.next;
            }
            head = head.next;
        }
        head.next = (l1 != null) ? l1 : l2;
        return sentinel.next;
    }
}
```
