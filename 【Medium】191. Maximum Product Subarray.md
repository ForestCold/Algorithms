> Find the contiguous subarray within an array (containing at least one number) which has the largest product.
>

**Example:** 

Given the array [−2,2,−3,4,−1,2,1,−5,3], the contiguous subarray [4,−1,2,1] has the largest sum = 6.

## 解题思路

思路和 [041. Maximum Subarray](https://github.com/ForestCold/Algorithms/blob/master/%E3%80%90Easy%E3%80%91041.%20Maximum%20Subarray.md)
类似，难点在于处理corner case的问题：

首先，考虑正负数，维护两个变量分别存储正数的最小值和负数的最大值，如果当前product为正数则除以最小正数，当前product为负数则除以最大负数。

第二，考虑0，如果遇到0则跳过，一切重新开始，product又回到1。但最后需要判断一下如果包含0并且跳过0后计算出来的max小于0，则返回0。

## 核心代码

        for (int i = 0; i < nums.length; i++){
            
            if (nums[i] == 0){
                
                hasZero = true;
                
                positiveMin = Integer.MAX_VALUE;
                negativeMax = Integer.MIN_VALUE;
                
                product = 1;
                
            } else {
                
                product = (i == 0) ? nums[i] : product * nums[i];
                
                if (product > max) max = product;
                else if (product > 0) max = Math.max(max, product / positiveMin);
                else if (product < 0) max = Math.max(max, product / negativeMax);
        
                positiveMin = (product > 0 && product < positiveMin) ? product : positiveMin;
                negativeMax = (product < 0 && product > negativeMax) ? product : negativeMax;
            
            }
        }
        
        if (hasZero && max < 0) return 0;


## 时间空间复杂度

O(n) + S(1)

*n为数组长度*
