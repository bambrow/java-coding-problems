# 138 Copy List with Random Pointer

```java
/*
A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.
*/

/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */

// 第一步，遍历链表并且讲所有元素的值复制一遍，间隔插入原链表中间；
// 比如 1 -> 2 -> 3 -> null 变成 1 -> 1 -> 2 -> 2 -> 3 -> 3 -> null；
// 第二步，复制随机指针，使得复制后的链表节点，其随机指针指向复制的同名节点；
// 最后将链表拆开恢复原样。
// 本题的做法不太容易用语言描述，一定要深入理解代码。

public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null) return null;
        RandomListNode cur = head;
        RandomListNode next = null;
        while (cur != null) {
            next = cur.next;
            cur.next = new RandomListNode(cur.label);
            cur.next.next = next;
            cur = next;
        }
        cur = head;
        RandomListNode copy = null;
        while (cur != null) {
            next = cur.next.next;
            copy = cur.next;
            copy.random = cur.random == null ? null : cur.random.next;
            cur = next;
        }
        RandomListNode newHead = head.next;
        cur = head;
        while (cur != null) {
            next = cur.next.next;
            copy = cur.next;
            cur.next = next;
            copy.next = next == null ? null : next.next;
            cur = next;
        }
        return newHead;
    }
}
```
