> Given an integer array, heapify it into a min-heap array.
>
> For a heap array A, A[0] is the root of heap, and for each A[i], A[i * 2 + 1] is the left child of A[i] and A[i * 2 + 2] is the right child of A[i].
>
> **Clarification**
>
> What is heap?
>
> Heap is a data structure, which usually have three methods: push, pop and top. where "push" add a new element the heap, "pop" delete the minimum/maximum element in the heap, "top" return the minimum/maximum element.
>
> What is heapify?
>
> Convert an unordered integer array into a heap array. If it is min-heap, for each element A[i], we will get A[i * 2 + 1] >= A[i] and A[i * 2 + 2] >= A[i].
>
> What if there is a lot of solutions?
>
> Return any of them.

**Example**

Given [3,2,1,4,5], return [1,2,3,4,5] or any legal heap array.

## 解题思路

从第一层非叶子节点开始往上遍历调整堆结构。每次找出root和左右孩子中的最小值，如果最小值不是root则将它与root进行交换，然后从它开始往下依次重复这个过程，
直到遍历到叶子节点或者root就是最小值为止。因为是从下往上调整的所以保证了当root是最小值时，以它左右孩子为跟节点的树都已经满足堆的条件。

## 核心代码
        
        // 遍历非叶子节点
        for (int i = A.length / 2 - 1; i >= 0; i--){
            
            int root = i, smallest = root;
            
            while (root < A.length){
                
                int left = root * 2 + 1 < A.length ? root * 2 + 1 : -1;
                int right = root * 2 + 2 < A.length ? root * 2 + 2 : -1;
                
                if (left != -1 && A[left] < A[smallest]) smallest = left;
                if (right != -1 && A[right] < A[smallest]) smallest = right;
                if (smallest == root) break;
                
                int tmp = A[smallest];
                A[smallest] = A[root];
                A[root] = tmp;
                root = smallest;
                
            }
        }

## 时间空间复杂度

O(n) + S(1)



