# 82 Remove Duplicates from Sorted List II

```java
/*
Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

For example,
Given 1->2->3->3->4->4->5, return 1->2->5.
Given 1->1->1->2->3, return 2->3.
*/

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

// 方法与83类似，然而这次是有重复就全部删除。我们需要在表头之前建立一个哨兵，以应对表头被删除的情况。
// 使用prev追踪当前节点之前的位置，因为要删除重复节点，prev需要跨过所有重复的节点。
// cur不停地跳过所有有重复的节点。
// 注意循环外还要设置一下最终prev.next的指向，这时候，cur有可能指向最后一个节点，也有可能指向null。

class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) return head;
        ListNode cur = head;
        ListNode sentinel = new ListNode(0);
        ListNode prev = sentinel;
        while (cur != null && cur.next != null) {
            if (cur.val == cur.next.val) {
                while (cur.next != null && cur.val == cur.next.val) cur = cur.next;
            }
            else {
                prev.next = cur;
                prev = prev.next;
            }
            cur = cur.next;
        }
        prev.next = cur;
        return sentinel.next;
    }
}
```
