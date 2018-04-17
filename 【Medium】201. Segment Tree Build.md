> The structure of Segment Tree is a binary tree which each node has two attributes start and end denote an segment / interval.
>
> start and end are both integers, they should be assigned in following rules:
>
> + The root's start and end is given by build method.
> + The left child of node A has start=A.left, end=(A.left + A.right) / 2.
> + The right child of node A has start=(A.left + A.right) / 2 + 1, end=A.right.
> + if start equals to end, there will be no children for this node.
> + Implement a build method with two parameters start and end, so that we can create a corresponding segment tree with every node has the correct start and end value, return the root of this segment tree.
>
> **Notice:** 
> 
> It's guaranteed that the size of the array is greater or equal to k.
>
> **Clarification**
>
> Segment Tree (a.k.a Interval Tree) is an advanced data structure which can support queries like:
>
> + which of these intervals contain a given point
> + which of these points are in a given interval

**Example:** 

Given start=0, end=3. The segment tree will be:

                   [0,  3]
                 /        \
          [0,  1]           [2, 3]
          /     \           /     \
       [0, 0]  [1, 1]     [2, 2]  [3, 3]
   
Given start=1, end=6. The segment tree will be:

                   [1,  6]
                 /        \
          [1,  3]           [4,  6]
          /     \           /     \
       [1, 2]  [3,3]     [4, 5]   [6,6]
       /    \           /     \
    [1,1]   [2,2]     [4,4]   [5,5]

## 解题思路

Segment Tree(线段树) 是一种可以用来进行基于区间的操作的数据结构，所有满足结合律的操作都可以在Segment Tree上进行（比如元素出现次数、最大值、最小值etc.）。
创建、修改和查询Segment Tree的时间复杂度都是logn级别的，所以如果一道题能被转化成求在某个范围内满足某种条件，都可以用Segment Tree来做（比如找出比某个数大的，小的etc.）。

这题的follow up：
 + 247 Segment Tree Query I
 + 248 Count of Smaller Number
 + 249 Count of Smaller Number before itself 

## 核心代码

    public SegmentTreeNode build(int start, int end) {
        // write your code here
        
        if (start > end){
            return null;
        }
        
        SegmentTreeNode node = new SegmentTreeNode(start, end);
        
        if (start == end){
            node.left = node.right = null;
        } else {
            int mid = start + (end - start) / 2;
            node.left = build(start, mid);
            node.right = build(mid + 1, end);
        }
        
        return node;
    }


## 时间空间复杂度

O(logn)

*n为end-start*
