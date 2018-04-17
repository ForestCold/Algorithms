> Give you an integer array (index from 0 to n-1, where n is the size of this array, data value from 0 to 10000) . For each element Ai in the array, count the number of element before this element Ai is smaller than it and return count number array.
>
> **Notice:** 
> 
> We suggest you finish problem Segment Tree Build, Segment Tree Query II and Count of Smaller Number first.
>

**Example:** 

For array [1,2,7,8,5], return [0,1,2,3,2]

## 解题思路

先求出数组的最大值和最小值，以此为区间建一棵空的Segment Tree。
之后遍历扫描数组，每次查询后将新的元素加入Segment Tree中，加入的时候只需要修改包含这个元素的节点。

 + 建树过程： [201. Segment Tree Build](https://github.com/ForestCold/Algorithms/blob/master/%E3%80%90Medium%E3%80%91201.%20Segment%20Tree%20Build.md)
 + 查询过程： [247. Segment Tree Query II](https://github.com/ForestCold/Algorithms/blob/master/%E3%80%90Medium%E3%80%91247.%20Segment%20Tree%20Query%20II.md)

## 核心代码

插入过程：
    
    private void insertNodeToSegmentTree(TreeNode root, int target){
        if (root == null) return;
        if (root.start <= target && root.end >= target){
            root.count += 1;
            insertNodeToSegmentTree(root.left, target);
            insertNodeToSegmentTree(root.right, target);
        }
    }


## 时间空间复杂度

O(nlog(max - min))

*n为数组长度*
