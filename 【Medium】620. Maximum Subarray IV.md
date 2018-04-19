> Given an integer arrays, find a contiguous subarray which has the largest sum and length should be greater or equal to given length k.
> Return the largest sum, return 0 if there are fewer than k elements in the array.
> **Notice:** 
> 
> Ensure that the result is an integer type.
>

**Example:** 

Given the array [-2,2,-3,4,-1,2,1,-5,3] and k = 5, the contiguous subarray [2,-3,4,-1,2,1] has the largest sum = 5.

## 解题思路

在
[41. Maximum Subarray](https://github.com/ForestCold/Algorithms/blob/master/%E3%80%90Easy%E3%80%9141.%20Maximum%20Subarray.md)
中已经做过找出某个最大sum的子数组问题。这题唯一的不同在于限制了数组的长度必须大于等于k，别的思路完全一致。因此做法和41题唯一的不同之处在于min的取值和更新，
由于Sum[i] - Sum[j]中的j只能在0到i-k之间取（这样才能保证数组长度大于k），因此再设置一个变量指向Sum[i-k]，用它来更新当前的min。

需要注意的是min的初始值问题，要考虑这个数组包含第一个元素的情况，可以把min的初始值设置为0并在i >= k的时候才开始更新min值，
也可以把min的初始值设置为正无穷但在i - k = -1时将其置为0。

这题的follow up：

## 核心代码
        
        int sum = 0, sumIminusK = 0, min = 0, max = Integer.MIN_VALUE;
        
        for (int i = 0; i < nums.length; i++){
            sum = (i == 0) ? nums[i] : sum + nums[i];
            if (i >= k) sumIminusK = (i == k) ? nums[0] : sumIminusK + nums[i - k];
            min = Math.min(sumIminusK, min);
            if (i >= k - 1) max = Math.max(sum - min, max);
        }


## 时间空间复杂度

O(n) + S(1)

*n为数组长度*
