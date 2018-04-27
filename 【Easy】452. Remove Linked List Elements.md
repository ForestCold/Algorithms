> Remove all elements from a linked list of integers that have value val.
>
> **Notice:** 
>+ Given 1->2->3->3->4->5->3, val = 3, you should return the list as 1->2->4->5

**Example:** 

Given a=1 and b=2 return 3

## 解题思路

略。

## 核心代码

        while (point != null) {
            if (point.val == val) {
                prev.next = point.next;
            } else {
                prev = point;
            }
            point = point.next;
        }

## 时间空间复杂度

O(n) + S(1)

