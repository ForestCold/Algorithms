> Given a non-negative integer represented as non-empty a singly linked list of digits, plus one to the integer.
>
> You may assume the integer do not contain any leading zero, except the number 0 itself.
>
> The digits are stored such that the most significant digit is at the head of the list.
>

**Example:** 

Given head = 1 -> 2 -> 3 -> null, return 1 -> 2 -> 4 -> null.

## 解题思路

递归进位。

## 核心代码

    private int helper(ListNode node){
        
        int sum = 0;
        
        if (node.next == null) sum = node.val + 1;
        else sum = node.val + helper(node.next);
        
        node.val = sum % 10;
        
        return sum / 10;
    }

## 时间空间复杂度

O(n) + S(1)
