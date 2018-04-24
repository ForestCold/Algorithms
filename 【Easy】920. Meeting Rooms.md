> Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), determine if a person could attend all meetings.
>

**Example:** 

Given intervals = [[0,30],[5,10],[15,20]], return false.

## 解题思路

复习sort的comparator。

## 核心代码
        
        Collections.sort(intervals, new Comparator<Interval>(){
            @Override
            public int compare(Interval a, Interval b){
                return a.start < b.start ? -1 : (a.start > b.start ? 1 : 0);
            }
        });


## 时间空间复杂度

O(nlogn) + S(n)

*n为数组长度的两倍*
