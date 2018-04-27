> Find the middle node of a linked list.
>

**Example:** 

Given 1->2->3, return the node with value 2.

Given 1->2, return the node with value 1.

## 解题思路

略。

## 核心代码

        ListNode slow = dummy, fast = dummy;
        
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        return slow;

## 时间空间复杂度

O(n) + S(1)

