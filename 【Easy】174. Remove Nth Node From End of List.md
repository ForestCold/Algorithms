> Given a linked list, remove the nth node from the end of list and return its head.
>
> **Notice:** 
>+ The minimum number of nodes in list is n.

**Example:** 

Given linked list: 1->2->3->4->5->null, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5->null.

## 解题思路

唯一要注意的是slow和fast的初始值。

## 核心代码

        ListNode slow = dummy, fast = dummy;
        
        for (int i = 0; i < n; i++) {
            fast = fast.next;
        }
        
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next;
        }
        
        slow.next = slow.next.next;

## 时间空间复杂度

O(n) + S(1)

