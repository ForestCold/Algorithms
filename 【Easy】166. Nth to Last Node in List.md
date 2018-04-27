> Find the nth to last element of a singly linked list. 
>
> The minimum number of nodes in list is n.
>

**Example:** 

Given a List  3->2->1->5->null and n = 2, return node  whose value is 1.

## 解题思路

维护两个相差为n个node的指针。

## 核心代码

        for (int i = 0; i < n; i++) {
            fast = fast.next;
        }
        
        while (fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next;
        }

## 时间空间复杂度

O(n) + S(1)


