> Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

**Example:** 

Given 1->2->3->3->4->4->5, return 1->2->5.

Given 1->1->1->2->3, return 2->3.

## 解题思路

slow保存当前监测到的node，fast保存slow之后有重复值的最后一个node。要注意的是如果要删值，不要再把slow往后移一格。

## 核心代码

        ListNode slow = dummy, fast = head;
        
        while (fast != null && fast.next != null) {
            if (fast.next != null && fast.next.val == fast.val) {
                while (fast.next != null && fast.next.val == fast.val) fast = fast.next;
                slow.next = fast.next;
            } else slow = slow.next;
            fast = slow.next;
        }

## 时间空间复杂度

O(n) + S(1)

