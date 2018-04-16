> Divide two integers without using multiplication, division and mod operator. If it is overflow, return 2147483647

**Example:** 

Given dividend = 100 and divisor = 9, return 11.

## 解题思路

对于被除数m和除数n，可以写成m = n * (a1 * 2^0 + a2 * 2^1 + ... + ax * 2 ^ x)的形式。因此通过一个循环，首先找出使得 n * 2^i <= m 的最大i, 
比如11 / 3, 3 * 2^1 = 6， 3 * 2^2 = 12 > 11, 所以2^1是要求的最大数。之后将2^1加入结果，并用11-6替换原来的11，
再进行第二次循环：3 * 2^0 = 3 < 5, 将2 ^ 0加入结果，剩下的2小于被除数3了，表示2是余数，停止循环。

## 核心代码

a是被除数，b是除数，k是上述讨论的最大的2^i，外循环判断是否只剩下余数，内循环寻找最大的k。
      
        while (a >= b){
            c = b;
            k = 1;
            while (a >= c){
                c = c << 1;
                k = k << 1;
            }
            result += k >> 1;
            a -= c >> 1;            
        }

## 时间空间复杂度

约等于O(log(a/b))

