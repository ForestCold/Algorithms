> For an array, we can build a SegmentTree for it, each node stores an extra attribute count to denote the number of elements in the the array which value is between interval start and end. (The array may not fully filled by elements)
>
> **Notice:** 
> 
> It is much easier to understand this problem if you finished Segment Tree Buildand Segment Tree Query first.
>

**Example:** 

For array [0, 2, 3], the corresponding value Segment Tree is:

                         [0, 3, count=3]
                         /             \
              [0,1,count=1]             [2,3,count=2]
              /         \               /            \
       [0,0,count=1] [1,1,count=0] [2,2,count=1], [3,3,count=1]
   
query(1, 1), return 0

query(1, 2), return 1

query(2, 3), return 2

query(0, 2), return 2

## 解题思路

如果查询区间与当前区间不重叠返回0，如果查询区间包含当前区间返回当前区间的值，如果有交集切分递归。

建树操作：

 + [201. Segment Tree Build](https://github.com/ForestCold/Algorithms/edit/master/%E3%80%90Medium%E3%80%91201.%20Segment%20Tree%20Build.md)

这题的follow up：
 + [248 Count of Smaller Number](https://github.com/ForestCold/Algorithms/blob/master/%E3%80%90Medium%E3%80%91248.%20Count%20of%20Smaller%20Number%20.md)
 + [249 Count of Smaller Number before itself ](https://github.com/ForestCold/Algorithms/blob/master/%E3%80%90Hard%E3%80%91249.%20Count%20of%20Smaller%20Number%20before%20itself.md)

## 核心代码

    public int query(SegmentTreeNode root, int start, int end) {     
        if (root == null || root.start > end || root.end < start) return 0;
        if (start <= root.start && end >= root.end) return root.count;
        return query(root.left, start, end) + query(root.right, start, end);
    }


## 时间空间复杂度

O(logn)

*n为end-start*
