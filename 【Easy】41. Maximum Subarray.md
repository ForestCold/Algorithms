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

## 核心代码

        for (int i = 0; i < nums.length; i++){
            prefixSum += nums[i]; //更新sum[i]
            max = Math.max(prefixSum - min, max); //更新当前最大值
            min = Math.min(prefixSum, min); //更新当前前序和的最小值
        }


## 时间空间复杂度

O(n) + S(1)

*n为数组长度*
