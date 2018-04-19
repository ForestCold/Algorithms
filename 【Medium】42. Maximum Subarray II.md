> Given an array of integers, find two non-overlapping subarrays which have the largest sum.
> The number in each subarray should be contiguous.
> Return the largest sum.
> **Notice:** 
> 
> The subarray should contain at least one number.
>

**Example:** 

For given [1, 3, -1, 2, -1, 2], the two subarrays are [1, 3] and [2, -1, 2] or [1, 3, -1, 2] and [2], 
they both have the largest sum 7.

## 解题思路

在
[41. Maximum Subarray](https://github.com/ForestCold/Algorithms/blob/master/%E3%80%90Easy%E3%80%9141.%20Maximum%20Subarray.md)
中已经做过找出某个最大sum的子数组问题。这题要求两个不相交的最大和子数组，则可以对分割线进行扫描。
首先用两个数组left和right记录从左向右扫描的最大子数组和和从右向左扫描的最大子数组和，即left[i]表示0到i之间的最大子数组和，right[i]表示i到n - 1之间的最大子数组和。当扫描分割线时，left[i]表示分割线左边能取到的最大子数组和，
right[i + 1]表示分割线右边能取到的最大子数组和。

这题的follow up：

## 核心代码
        
扫描分割线：
        
        max = Integer.MIN_VALUE;
        for (int i = 0; i < nums.size() - 1; i++){
            max = Math.max(max, left[i] + right[i + 1]);
        }


## 时间空间复杂度

O(n) + S(n)

*n为数组长度*
