> Given a linked list, swap every two adjacent nodes and return its head.
>

**Example:** 

Given 1->2->3->4, you should return the list as 2->1->4->3.

## 解题思路

错位设置指针的值，比如12反向，34反向，指针的值应该是01->23的顺序。

## 核心代码

        ListNode left = dummy, right = dummy.next;
        
        while (right != null && right.next != null) {
            left.next = right.next;
            right.next = left.next.next;
            left.next.next = right;
            left = right;
            right = right.next;
        }

## 时间空间复杂度

O(n) + S(1)

