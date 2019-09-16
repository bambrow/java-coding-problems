# 160 Intersection of Two Linked Lists

```java
/*
Write a program to find the node at which the intersection of two singly linked lists begins.


For example, the following two linked lists:

A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗
B:     b1 → b2 → b3
begin to intersect at node c1.


Notes:

If the two linked lists have no intersection at all, return null.
The linked lists must retain their original structure after the function returns.
You may assume there are no cycles anywhere in the entire linked structure.
Your code should preferably run in O(n) time and use only O(1) memory.
*/

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */

// 本题判断两个无环链表是否相交，如果是返回交点。我们首先遍历遍历链表A并且停在最后一个节点。
// 遍历的同时记录链表A的长度。然后遍历链表B，同样停留在尾节点，并且记录长度。
// 在本题我们统一用n表示A与B长度的差值。
// 如果两个尾节点不同，那么不相交；否则，重新回到头部，让长度长的那个链表先走相当于两链表长度差值的步数。
// 然后两个链表同时继续遍历，它们一定会在交汇点相遇。

public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) return null;
        ListNode cur1 = headA;
        ListNode cur2 = headB;
        int n = 0;
        while (cur1.next != null) {
            n++;
            cur1 = cur1.next;
        }
        while (cur2.next != null) {
            n--;
            cur2 = cur2.next;
        }
        if (cur1 != cur2) return null;
        cur1 = n > 0 ? headA : headB;
        cur2 = cur1 == headA ? headB : headA;
        if (n < 0) n = -n;
        while (n != 0) {
            n--;
            cur1 = cur1.next;
        }
        while (cur1 != cur2) {
            cur1 = cur1.next;
            cur2 = cur2.next;
        }
        return cur1;
    }
}
```
