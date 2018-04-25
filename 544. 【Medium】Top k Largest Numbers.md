> Given an integer array, find the top k largest numbers in it.
>

**Example:** 

Given [3,10,1000,-99,4,100] and k = 3.
Return [1000, 100, 10].

## 解题思路

略。

## 核心代码

        for (int i = 0; i < nums.length; i++){
            pq.add(nums[i]);
            if (pq.size() > k)pq.remove(pq.peek());
        }

## 时间空间复杂度

O(nlogk) + S(k)

*n为数组长度*


