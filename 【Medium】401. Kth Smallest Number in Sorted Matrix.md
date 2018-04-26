> Find the kth smallest number in at row and column sorted matrix.
>

**Example:** 

Given k = 4 and a matrix:

    [
      [1 ,5 ,7],
      [3 ,7 ,8],
      [4 ,8 ,9],
    ]

return 5

## 解题思路

剪枝条件：如果当前值已经大于找到的第k个值，就不再访问它右边和下面的元素。为了从小到大进行访问，用一个queue来从左上角向右下角扫描。

## 核心代码

        int i = 0, j = 0, n = matrix[0].length;
        queue.offer(i * n + j);
        
        while (queue.size() > 0){
            int head = queue.poll();
            i = head / n;
            j = head % n;
            if (pq.size() >= k && -1 * matrix[i][j] < pq.peek()) continue;
            pq.add(-1 * matrix[i][j]);
            if (i + 1 < matrix.length && !queue.contains((i + 1) * n + j)) queue.add((i + 1) * n + j);
            if (j + 1 < matrix[0].length && !queue.contains(i * n + j + 1)) queue.add(i * n + j + 1);
            if (pq.size() > k) pq.remove(pq.peek());
        }
        
## 时间空间复杂度

O(k) + S(1)



