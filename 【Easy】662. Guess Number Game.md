> We are playing the Guess Game. The game is as follows:
> I pick a number from 1 to n. You have to guess which number I picked.
> Every time you guess wrong, I'll tell you whether the number is higher or lower.
> You call a pre-defined API guess(int num) which returns 3 possible results (-1, 1, or 0):
>


**Example:** 

n = 10, I pick 4 (but you don't know)

Return 4. Correct !

## 解题思路

常规二分法。

## 时间空间复杂度

O(nlogn) + S(1)

