> Given an array with integers.
>
> Find two non-overlapping subarrays A and B, which |SUM(A) - SUM(B)| is the largest.
>
> Return the largest difference.
>
> **Notice:** 
> 
> The subarray should contain at least one number.
>

**Example:** 

For [1, 2, -3, 1], return 6.

## 解题思路

和
[042. Maximum Subarray II](https://github.com/ForestCold/Algorithms/blob/master/%E3%80%90Medium%E3%80%91042.%20Maximum%20Subarray%20II.md)
类似，求两个没有交集的子数组问题，想到扫描分割线。先求出四个数组leftMin, leftMax, rightMin, rightMax，
分别存储从左向右扫描到当前位置的最大sum、最小sum, 和从右向左扫描到当前位置的最大sum、最小sum。之后和42题一样扫描分割线找出结果。

## 核心代码

        max = Integer.MIN_VALUE;
        for (int i = 0; i < nums.length - 1; i++){
            max = Math.max(max, Math.max(leftMax[i] - rightMin[i + 1], rightMax[i + 1] - leftMin[i]));
        }


## 时间空间复杂度

O(n) + S(n)

*n为数组长度*
