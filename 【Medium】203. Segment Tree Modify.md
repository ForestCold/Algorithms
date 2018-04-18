> For a Maximum Segment Tree, which each node has an extra value max to store the maximum value in this node's interval.
>
>Implement a modify function with three parameter root, index and value to change the node's value with [start, end] = [index, index] to the new given value. Make sure after this change, every node in segment tree still has the max attribute with the correct value.
>
> **Notice:** 
> 
> We suggest you finish problem Segment Tree Build and Segment Tree Query first.
>

**Example:** 

For segment tree:

                             [1, 4, max=3]
                          /                \
              [1, 2, max=2]                [3, 4, max=3]
             /              \             /             \
      [1, 1, max=2], [2, 2, max=1], [3, 3, max=0], [4, 4, max=3]
    
if call modify(root, 2, 4), we can get:
    
                             [1, 4, max=4]
                          /                \
              [1, 2, max=4]                [3, 4, max=3]
             /              \             /             \
      [1, 1, max=2], [2, 2, max=4], [3, 3, max=0], [4, 4, max=3]
 
    
or call modify(root, 4, 0), we can get:
   
                             [1, 4, max=2]
                          /                \
              [1, 2, max=2]                [3, 4, max=0]
             /              \             /             \
      [1, 1, max=2], [2, 2, max=1], [3, 3, max=0], [4, 4, max=0]

## 解题思路

略。

## 核心代码

        if (root == null || index < root.start || index > root.end) return;
        if (root.start == index && root.end == index) {
            root.max = value;
            return;
        }
        
        modify(root.left, index, value);
        modify(root.right, index, value);

        root.max = Math.max(root.left.max, root.right.max);


## 时间空间复杂度

O(logn)

*n为end-start*

