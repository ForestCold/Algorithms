> You have two numbers represented by a linked list, where each node contains a single digit. The digits are stored in reverse order, such that the 1's digit is at the head of the list. Write a function that adds the two numbers and returns the sum as a linked list.
>

**Example:** 

Given 7->1->6 + 5->9->2. That is, 617 + 295.

Return 2->1->9. That is 912.

Given 3->1->5 and 5->9->2, return 8->0->8.

## 解题思路

模拟加法器的进位过程，每次把carry加到下一位上。

## 核心代码

        while (head1 != null && head2 != null) {
            int sum = head1.val + head2.val + carry;
            carry = sum / 10;
            head.next = new ListNode(sum % 10);
            head = head.next;
            head1 = head1.next;
            head2 = head2.next;
        }
        
        while (head1 != null) {
            int sum = head1.val + carry;
            carry = sum / 10;
            head.next = new ListNode(sum % 10);
            head1 = head1.next;
            head = head.next;
        }
        
        while (head2 != null) {
            int sum = head2.val + carry;
            carry = sum / 10;
            head.next = new ListNode(sum % 10);
            head2 = head2.next;
            head = head.next;
        }
        
        if (carry != 0) head.next = new ListNode(carry);
        
## 时间空间复杂度

O(m + n) + S(1)

*m和n为两个链表长度*



