> Implement double sqrt(double x) and x >= 0. Compute and return the square root of x.
>
> **Notice:** 
>+ You do not care about the accuracy of the result, we will help you to output results.

**Example:** 

Given n = 2 return 1.41421356

## 解题思路

用二分法进行查找，需要注意的是对于0到1之间的数，开方上下界为[0, 1]，而大于1的数，开方上下界为[0, x]。

## 时间空间复杂度

O(Max(logn), 精度位数) + S(1)

*n为x*
