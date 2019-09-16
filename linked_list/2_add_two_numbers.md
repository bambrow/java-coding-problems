# 2 Add Two Numbers

```java
/*
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
*/

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

// 本题链表中的数反转，结果也反转。例题中实际为342+465=807。
// 从左至右加和即可。注意进位加入下一个ListNode的val值中。
// 使用三个ListNode变量，其中有一个哨兵。
// 如果链表中的数是正向存储呢？先反转链表。反转链表只需要O(n)。
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {

        ListNode prev = new ListNode(0);
        ListNode sentinel = prev;
        ListNode cur = null;
        int addUp = 0;

        while (l1 != null || l2 != null || addUp != 0) {
            cur = new ListNode(0);
            int sum = ((l1 == null) ? 0 : l1.val) + ((l2 == null) ? 0 : l2.val) + addUp;
            cur.val = sum % 10;
            addUp = sum / 10;
            prev.next = cur;
            prev = cur;
            l1 = (l1 == null) ? l1 : l1.next;
            l2 = (l2 == null) ? l2 : l2.next;
        }

        return sentinel.next;

    }
}
```
