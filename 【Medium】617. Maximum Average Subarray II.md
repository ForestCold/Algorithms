> Given an array with positive and negative numbers, find the maximum average subarray which length should be greater or equal to given length k.
>
> **Notice:** 
>+ It's guaranteed that the size of the array is greater or equal to k.

**Example:** 

Given nums = [1, 12, -5, -6, 50, 3], k = 3

Return 15.667 // (-6 + 50 + 3) / 3 = 15.667

## 解题思路

用二分法进行夹逼。因为子数组的平均值一定在数组最大值和最小值之间，因此每次判断是否存在子数组使得平均值大于mid，如果存在，则向mid->max收敛，否则向min->mid收敛。

查询是否存在满足这样条件的子数组可以用prefiSum（前序和），prefixSum[i]指的是数组arr中从0到i的所有元素之和。满足条件的prefixSum[i]需要：
+ prefixSum[i] / ((i + 1) * mid) - prefixSum[j] / ((j + 1) * mid) >= 0 
+  i - j >=k

用一个循环计算prefixSum[i]，并且维护一个变量保存从0到i - k的最小prefixSum值（减数越小结果越大）。
当指针向后移，试图更新最小值的时候直接比较之前计算出的最小值和i - k + 1处的prefixSum值。
为了降低空间复杂度，直接用变量而不是数组存储prefixSum。

## 核心代码

返回类型:

    class ResultType {
        boolean exist;
        int low;
        int high;
        ResultType(boolean e, int l, int h){
            this.exist = e;
            this.low = l;
            this.high = h;
        }
    }
    
测试是否存在平均值大于等于mid的子数组:

    private ResultType canFind(int[] nums, float mid, int k){
        
        float prefixSumI = nums[0];
        float prefixSumIminuxK = 0;
        float Min = 0;
        int minIndex = -1;

        for (int i = 1; i < nums.length; i++){
            prefixSumI += nums[i]; 
            if (i >= k){
                prefixSumIminuxK += nums[i - k];
            }
            if (i + 1 >= k && (prefixSumIminuxK - (i + 1 - k) * mid) <= Min){
                Min = prefixSumIminuxK - (i + 1 - k) * mid;
                minIndex = i - k + 1;
            }
            if (minIndex >= 0 && (prefixSumI - (i + 1) * mid) - Min >= 0){
                return new ResultType(true, minIndex, i);
            }
        }
        
        return new ResultType(false, -1, -1);
        
    }


## 时间空间复杂度

O(n) + S(1)

*n为数组长度*
