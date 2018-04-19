> Given an integer array, find a subarray with sum closest to zero. Return the indexes of the first number and last number.
>

**Example:** 

Given [-3, 1, 1, -3, 5], return [0, 2], [1, 3], [1, 1], [2, 2] or [0, 4].

## 解题思路

相当于求最接近的Sum[i]和Sum[j]。计算处Sum数组后将其排序，两两比较找到最接近的一对，返回它们对应的坐标。
需要注意的是如果在计算Sum数组的时候就发现和之前某个Sum值相等，直接返回当前Sum和那个Sum的下标。

## 核心代码

        for (int i = 1; i < sum.length; i++){
            if (sum[i] - sum[i - 1] < min){
                min = sum[i] - sum[i - 1];
                result[0] = Math.min(map.get(sum[i - 1]), map.get(sum[i])) + 1;
                result[1] = Math.max(map.get(sum[i - 1]), map.get(sum[i]));
            }
        }


## 时间空间复杂度

O(n) + S(n)

*n为数组长度*
