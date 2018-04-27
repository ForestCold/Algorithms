> Implement a function to check if a linked list is a palindrome.

**Example:** 

Given 1->2->1, return true

## 解题思路

这个做法不是S(1)的做法，如果要实现S(1)，可以先用双指针找到链表中点，然后反转后半段链表，再用双指针挨个比较。

## 核心代码

        // stack 做法
        while (h1 != null) {
            stack.push(h1.val);
            h1 = h1.next;
        }
        
        while (stack.size() > 0) {
            if (stack.pop() != h2.val) return false;
            h2 = h2.next;
        }
        
        // 反转 prev -> curt -> tmp
        while (curt != null){
          node tmp = curt.next;
          curt.next = prev;
          prev = curt;
          curt = tmp;
        }

## 时间空间复杂度

O(n) + S(n)

