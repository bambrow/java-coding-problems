# 206 Reverse Linked List

```java
/*
Reverse a singly linked list.

click to show more hints.

Hint:
A linked list can be reversed either iteratively or recursively. Could you implement both?
*/

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

// 简单题，直接看代码吧。

class Solution {
    public ListNode reverseList(ListNode head) {
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
}
```
