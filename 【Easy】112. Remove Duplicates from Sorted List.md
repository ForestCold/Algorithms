> Given a sorted linked list, delete all duplicates such that each element appear only once.
>

**Example:** 

Given 1->1->2, return 1->2.
Given 1->1->2->3->3, return 1->2->3.

## 解题思路

维护两个指针，slow指向当前检测到的元素，fast指向slow之后第一个和slow不一样的元素。

## 核心代码

        while (slow != null){
            while (fast != null && slow.val == fast.val){
                if (fast.next != null) fast = fast.next;
                else fast = null;
            }
            slow.next = fast;
            slow = fast;
        }

## 时间空间复杂度

O(n) + S(1)


