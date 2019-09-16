# 147 Insertion Sort List

```java
/*
Sort a linked list using insertion sort.

*/

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

// 中等难度。可能需要换头，因此使用哨兵。首先找到待插入节点合适的位置（定位prev），随后保存后继节点（succ），将目标节点插入中间即可。

class Solution {
    public ListNode insertionSortList(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode sentinel = new ListNode(0);
        ListNode prev = sentinel;
        ListNode cur = head;
        while (cur != null) {
            prev = sentinel;
            while (prev.next != null && prev.next.val <= cur.val) prev = prev.next;
            ListNode succ = prev.next;
            prev.next = cur;
            cur = cur.next;
            prev.next.next = succ;
        }
        return sentinel.next;
    }
}
```
