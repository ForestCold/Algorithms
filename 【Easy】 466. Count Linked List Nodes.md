> Find the middle node of a linked list.
>

**Example:** 

Given 1->3->5, return 3.

## 解题思路

略。

## 核心代码

        while (head != null) {
            head = head.next;
            count++;
        }

## 时间空间复杂度

O(n) + S(1)

