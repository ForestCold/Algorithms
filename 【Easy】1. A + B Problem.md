> Write a function that add two numbers A and B. You should not use + or any arithmetic operators.
>
> **Notice:** 
>+ There is no need to read data from standard input stream. Both parameters are given in function aplusb, you job is to calculate the sum and return it.

**Example:** 

Given a=1 and b=2 return 3

## 解题思路

a ^ b就是a和b相加之后，该进位的地方不进位的结果。a & b就是a和b里都是1的那些位置，a & b << 1 就是进位。计算过程实际上是当进位不为0的时候，
不停地将进位与原数字相加，再算出新的进位，直到进位为0。

## 核心代码

        while (b != 0){
            int _a = a ^ b;
            int _b = (a & b) << 1;
            a = _a;
            b = _b;
        }



