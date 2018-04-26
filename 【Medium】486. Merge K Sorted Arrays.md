> Given k sorted integer arrays, merge them into one sorted array.
>

**Example:** 

Given 3 sorted arrays:

    [
      [1, 3, 5, 7],
      [2, 4, 6],
      [0, 8, 9, 10, 11]
    ]
    
return [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11].

## 解题思路

全部仍到PriorityQueue里，但我觉得维护k个指针和一个长度为k的pq时间复杂度会更低，不过没实践。

## 核心代码

略。

## 时间空间复杂度

O(nlogn) + S(n)
或
O(nlogk) + S(k)


