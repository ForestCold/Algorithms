> Given an integer array (index from 0 to n-1, where n is the size of this array), and an query list. Each query has two integers [start, end]. For each query, calculate the sum number between index start and end in the given array, return the result list.
> Implement a modify function with three parameter root, index and value to change the node's value with [start, end] = [index, index] to the new given value. Make sure after this change, every node in segment tree still has the max attribute with the correct value.
>
> **Notice:** 
> 
> We suggest you finish problem Segment Tree Build, Segment Tree Query and Segment Tree Modify first.
>

**Example:** 

For array [1,2,7,8,5], and queries [(0,4),(1,2),(2,4)], return [23,9,20]

## 解题思路

a. prefixSum前序和数组
b. Segment Tree

## 时间空间复杂度

a. O(n)建立 + O(1)查询 + S(n)
b. O(nlogn)建立(不确定) + O(n)查询 + S(nlogn)(不确定)

*n为数组长度*

