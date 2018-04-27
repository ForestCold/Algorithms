> You have two numbers represented by a linked list, where each node contains a single digit. The digits are stored in forward order, such that the 1's digit is at the head of the list. Write a function that adds the two numbers and returns the sum as a linked list.
>

**Example:** 

Given 6->1->7 + 2->9->5. That is, 617 + 295.

Return 9->1->2. That is, 912.

## 解题思路

两个stack存输入，一个stack存输出。

## 核心代码

        while (head1 != null) {
            stack1.push(head1);
            head1 = head1.next;
        }
        
        while (head2 != null) {
            stack2.push(head2);
            head2 = head2.next;
        }
        
        while (stack1.size() > 0 || stack2.size() > 0) {
            int first = stack1.size() > 0 ? stack1.pop().val : 0;
            int second = stack2.size() > 0 ? stack2.pop().val : 0;
            int sum = first + second + carry;
            carry = sum / 10;
            stack3.push(sum % 10);
        }
        
        if (carry != 0) stack3.push(carry);
        
        while (stack3.size() > 0) {
            head.next = new ListNode(stack3.pop());
            head = head.next;
        }

## 时间空间复杂度

O(n) + S(n)

