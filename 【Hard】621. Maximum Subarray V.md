> Given an integer arrays, find a contiguous subarray which has the largest sum and length should be between k1 and k2 (include k1 and k2).
> Return the largest sum, return 0 if there are fewer than k1 elements in the array.
> **Notice:** 
> 
> Ensure that the result is an integer type.
>

**Example:** 

Given the array [-2,2,-3,4,-1,2,1,-5,3] and k1 = 2, k2 = 4, the contiguous subarray [4,-1,2,1] has the largest sum = 6.

## 解题思路

在
[620. Maximum Subarray IV](https://github.com/ForestCold/Algorithms/blob/master/%E3%80%90Medium%E3%80%91620.%20Maximum%20Subarray%20IV.md)
中已经做过找出某个最大sum的子数组，并且这个子数组的长度大于k的问题。这题加了个条件，数组长度要在k1和k2之间。思路和之前的子数组题完全一致
，不同的是min的取值范围这次只考虑sum[i - k2]到sum[i - k1]之间的最小值。求这个最小值有好多种做法，比如刚学的segment tree，或者再做一个sum数组的sum数组。
这里用segment tree来完成。

需要注意的是min的初始值问题，要考虑这个数组有可能包含第一个元素的情况，即i - k2 < 0 并且 i - k1 >= -1。

## 核心代码
        
        int min = Integer.MAX_VALUE, max = Integer.MIN_VALUE;
        
        for (int i = 0; i < sum.length; i++){
            int left = i - k2, right = i - k1;
            if (right >= 0) min = query(root, left, right);
            if (left < 0 && right >= -1) min = Math.min(0, min);
            if (right >= -1) max = Math.max(sum[i] - min, max);
        }


## 时间空间复杂度

O(nlogn) + S(n)

*n为数组长度*
