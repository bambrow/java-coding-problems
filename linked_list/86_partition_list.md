# 86 Partition List

```java
/*
Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,
Given 1->4->3->2->5->2 and x = 3,
return 1->2->2->4->3->5.
*/

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

// 分别维护两个链表，一个所有的值小于x，另一个所有的值大于等于x，遍历原链表并进行挂载（此时相对顺序都不变）
// 然后将大数链表挂载到小数链表后面即可。

class Solution {
    public ListNode partition(ListNode head, int x) {
        ListNode smallSentinel = new ListNode(0);
        ListNode largeSentinel = new ListNode(0);
        ListNode small = smallSentinel;
        ListNode large = largeSentinel;
        while (head != null) {
            if (head.val < x) {
                small.next = head;
                small = small.next;
            } else {
                large.next = head;
                large = large.next;
            }
            head = head.next;
        }
        large.next = null;
        small.next = largeSentinel.next;
        return smallSentinel.next;
    }
}
```
