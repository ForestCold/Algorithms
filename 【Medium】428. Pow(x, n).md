> Implement pow(x, n).
>
> **Notice:** 
>+ You don't need to care about the precision of your answer, it's acceptable if the expected answer and your answer 's difference is smaller than 1e-3.

**Example:** 

Pow(2.1, 3) = 9.261

Pow(0, 1) = 0

Pow(1, 0) = 1

## 解题思路

递归计算，为了减小时间复杂度，每个递归中只算一次n/2。需要注意的是当n为负数时相当于求(1/x)的n次方，因此在最初判断一下n是不是负数，如果是n = -1 * n并且
x = 1 / x。特殊情况为当n是Integer.MIN_VALUE(-2147483648)时，乘以-1会溢出，因为int的范围是[-2147483648, 2147483647]，因此这种情况需要特殊处理。

## 时间空间复杂度

O(logn) + S(1)

