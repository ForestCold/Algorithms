> Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.
>

**Example:** 

Given intervals = [(0,30),(5,10),(15,20)], return 2.

## 解题思路

把所有的start time和end time都扔到一个数组中进行排序，之后从前向后遍历，维护一个count变量表示当前时刻需要都房间数量，当遇到start时加1，遇到end时减1。
遍历之后count的最大值即为需要申请的最大房间数。

## 核心代码
        
        int count = 0, max = Integer.MIN_VALUE;
        for (int i = 0; i < list.size(); i++){
            if (list.get(i).type == 1)count++;
            else count--;
            max = Math.max(count, max);
        }


## 时间空间复杂度

O(nlogn) + S(n)

*n为数组长度的两倍*
