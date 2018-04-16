> Implement int sqrt(int x).
> Compute and return the square root of x.

**Example:** 

sqrt(3) = 1

sqrt(4) = 2

sqrt(5) = 2

sqrt(10) = 3

## 解题思路

这题需要注意的是在二分过程中整数溢出的问题，所以先把x强制转换为long型。

## 时间空间复杂度

O(logn)
*n为数组长度*
