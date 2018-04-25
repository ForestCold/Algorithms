> Find K-th largest element in an array. and N is much larger than k.
>
> **Notice:** 
>+ You can swap elements in the array

**Example:** 

In array [9,3,2,4,8], the 3rd largest element is 4.

In array [1,2,3,4,5], the 1st largest element is 5, 2nd largest element is 4, 3rd largest element is 3 and etc.

## 解题思路

略。

## 核心代码

        for (int i = 0; i < nums.length; i++){
            pq.add(nums[i]);
            if (pq.size() > k) pq.remove(pq.peek());
        }

## 时间空间复杂度

O(nlogk) + S(k)





