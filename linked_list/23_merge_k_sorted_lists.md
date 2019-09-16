# 23 Merge k Sorted Lists

```java
/*
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

*/

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

// 困难题。选择的策略是两两合并。两两合并的代码在21，直接拿来用。
// 不停地两两合并直到n=1。这时候返回lists的第一个元素即可。
// 这里的难度在于如何确定边界，并且在奇数偶数情况下都适用。
// 我们首先选择sep为(n+1)/2。然后将i处的链表与i+sep处的合并。
// 接下来是选择i的上界。这里上界定为n/2，可以保证长度为偶数时遍历到一半，长度为奇数时遍历到正中间停止。
// 这样剩下的长度就是(n+1)/2，正好是sep的值。

class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists.length == 0) return null;
        int n = lists.length;
        while (n > 1) {
            int sep = 1 + (n-1)/2;
            for (int i = 0; i < n/2; i++) {
                lists[i] = mergeTwoLists(lists[i], lists[i+sep]);
            }
            n = sep;
        }
        return lists[0];
    }

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
