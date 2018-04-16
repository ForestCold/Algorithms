> Given an array nums containing n + 1 integers where each integer is between 1 and n (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.
>
> **Notice:** 
>+ You must not modify the array (assume the array is read only).
>+ You must use only constant, O(1) extra space.
>+ Your runtime complexity should be less than O(n^2).
>+ There is only one duplicate number in the array, but it could be repeated more than once.

**Example:** 

Given nums = [5,5,4,3,2,1] return 5
Given nums = [5,4,4,3,2,1] return 4

## 解题思路

1. 常规做法: sort+扫描
2. 二分法: 1到n二分，每个二分中扫描一次array，如果小于mid的元素个数大于等于mid则重复数在左边，反之在右边。
3. 转换成链表找环问题。index i上的数字j指向index j上的数字，例如[5,4,4,3,2,1]，5->1->4->2->4，这个链表出现了环，原因是两个不同位置的4同时指向了index为4的2。
所以环的交点之前的node就是要求的数。
4. 换位置。和2的思路相似，将每个数字与自己减1的位置的数字交换，直到发现两个要交换的数字相等，证明已经有一个相同的数字被从别的位置移过来了。(但我写的代码跑到52%左右会WA，目前还没发现原因)

## 核心代码
        
        // 链表找环
        int slow = 0, fast = 0, head = 0, prev = 0;
        
        // 找相遇点
        while ((slow == fast && slow == 0) || slow != fast){
            slow = nums[slow];
            fast = nums[nums[fast]];
        }
        
        // 找交集
        while (head != slow){
            prev = head;
            head = nums[head];
            slow = nums[slow];
        }


## 时间空间复杂度

1. O(nlogn) + S(1)
2. O(nlogn) + S(1)
3. O(n) + S(1)
4. O(n) + S(1)
*n为数组长度*
