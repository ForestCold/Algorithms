> Given an array of integers, find a contiguous subarray which has the largest sum.
>
> **Notice:** 
> 
> The subarray should contain at least one number.
>

**Example:** 

Given the array [−2,2,−3,4,−1,2,1,−5,3], the contiguous subarray [4,−1,2,1] has the largest sum = 6.

## 解题思路

用一个变量sum记录当前的前序和（即sum[i] = a[0] + ... + a[i]），因为a[i -> k + 1]的和为sum[i] - sum[k]，
所以当i固定时（即sum[i]固定时），当前最大值max为当前前序和sum[i]减去当前元素之前前序和的最小值min。

这题的follow up：

> [041. Maximum Subarray](https://github.com/ForestCold/Algorithms/blob/master/%E3%80%90Easy%E3%80%91041.%20Maximum%20Subarray.md)
>
>[042. Maximum Subarray II](https://github.com/ForestCold/Algorithms/blob/master/%E3%80%90Medium%E3%80%91042.%20Maximum%20Subarray%20II.md)
>
>[620. Maximum Subarray IV](https://github.com/ForestCold/Algorithms/blob/master/%E3%80%90Medium%E3%80%91620.%20Maximum%20Subarray%20IV.md)
>
>[621. Maximum Subarray V](https://github.com/ForestCold/Algorithms/blob/master/%E3%80%90Hard%E3%80%91621.%20Maximum%20Subarray%20V.md)

## 核心代码

        for (int i = 0; i < nums.length; i++){
            prefixSum += nums[i]; //更新sum[i]
            max = Math.max(prefixSum - min, max); //更新当前最大值
            min = Math.min(prefixSum, min); //更新当前前序和的最小值
        }


## 时间空间复杂度

O(n) + S(1)

*n为数组长度*
