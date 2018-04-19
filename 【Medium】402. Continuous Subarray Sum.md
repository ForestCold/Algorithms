> Given an integer array, find a continuous subarray where the sum of numbers is the biggest. Your code should return the index of the first number and the index of the last number. (If their are duplicate answer, return anyone)
>

**Example:** 

Give [-3, 1, 3, -3, 4], return [1,4].

## 解题思路

与[041. Maximum Subarray](https://github.com/ForestCold/Algorithms/blob/master/%E3%80%90Easy%E3%80%91041.%20Maximum%20Subarray.md)完全一致，只是需要保存最小值对应的数组下标。

## 时间空间复杂度

O(n) + S(1)

*n为数组长度*
