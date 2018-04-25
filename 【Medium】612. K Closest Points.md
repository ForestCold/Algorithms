> Given some points and a point origin in two dimensional space, find k points out of the some points which are nearest to origin.
Return these points sorted by distance, if they are same with distance, sorted by x-axis, otherwise sorted by y-axis.
>

**Example:** 

Given points = [[4,6],[4,7],[4,4],[2,5],[1,1]], origin = [0, 0], k = 3
return [[1,1],[2,5],[4,4]]

## 解题思路

略。

## 核心代码

        for (int i = 0; i < points.length; i++){
            double distance = Math.pow((points[i].x - origin.x), 2) + Math.pow((points[i].y - origin.y), 2);
            pq.add(new Distance(points[i], distance));
            if (pq.size() > k) pq.remove(pq.peek());
        }

## 时间空间复杂度

O(nlogk) + S(k)



