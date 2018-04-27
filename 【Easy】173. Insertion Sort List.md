> Sort a linked list using insertion sort.
>

**Example:** 

Given 1->3->2->0->null, return 0->1->2->3->null.

## 解题思路

要注意插入到第一个元素到情况。

## 核心代码

        while (i != null && i.next != null) {
            ListNode j = i.next;
            if (j != null && j.val < i.val) {
                ListNode post = dummy.next;
                ListNode prev = dummy.next;
                while (post != i.next && post.val < j.val) {
                    prev = post;
                    post = post.next;
                }
                i.next = j.next;
                if (prev.val < j.val) {
                    prev.next = j;
                    j.next = post;
                } else {
                    j.next = dummy.next;
                    dummy.next = j;
                }
            } else {
                i = i.next;
            }
        }

## 时间空间复杂度

O(n^2) + S(1)

