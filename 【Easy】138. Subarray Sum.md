> Given an integer array, find a subarray where the sum of numbers is zero. Your code should return the index of the first number and the index of the last number.
>
> **Notice:** 
> 
> There is at least one subarray that it's sum equals to zero.
>

**Example:** 

Given [-3, 1, 2, -3, 4], return [0, 2] or [1, 3].

## 解题思路

用一个集合存储已经计算过的sum，如果当前sum[i]和之前某个已经计算过的sum[j]相等，即sum[i] - sum[j] = 0，证明从j+1到i的数组段和为0。
需要注意的是包含0号元素的情况，因此当sum[i]本身为0时，表示从第0个到第i个元素组成的子数组和为0，直接返回。

## 核心代码

        for (int i = 0; i < nums.length; i++){
            sum[i] = (i == 0) ? nums[i] : sum[i - 1] + nums[i];
            if (sum[i] == 0){
                result.add(0);
                result.add(i);
                return result;
            }
            if (map.containsKey(sum[i])){
                result.add(map.get(sum[i]) + 1);
                result.add(i);
                return result;
            } 
            map.put(sum[i], i);
        }


## 时间空间复杂度

O(n) + S(1)

*n为数组长度*
