> There are two properties in the node student id and scores, to ensure that each student will have at least 5 points, find the average of 5 highest scores for each person.
>

## 解题思路

用 Map<Integer, PriorityQueue> 记录每个学生的分数。

## 核心代码

        for (int i = 0; i < results.length; i++){
            if (!map.containsKey(results[i].id)) map.put(results[i].id, new PriorityQueue<>());
            PriorityQueue pq = map.get(results[i].id);
            pq.add(results[i].score);
            if (pq.size() > 5) pq.remove(pq.peek());
        }
        
## 时间空间复杂度

O(n) + S(n)



