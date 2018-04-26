> Give two users' ordered online time series, and each section records the user's login time point x and offline time point y. Find out the time periods when both users are online at the same time, and output in ascending order.
>
> **Notice:** 
> + We guarantee that the length of online time series meet 1 <= len <= 1e6.
> + For a user's online time series, any two of its sections do not intersect.

**Example:** 

Given seqA = [(1,2),(5,100)], seqB = [(1,6)], return [(1,2),(5,6)].

    Explanation:
    In these two time periods (1,2),(5,6), both users are online at the same time.

Given seqA = [(1,2),(10,15)], seqB = [(3,5),(7,9)], return [].

    Explanation:
    There is no time period, both users are online at the same time.

## 解题思路

扫描线，当start的数量等于2时代表两个用户都在线，开始计算时间，直到一个用户下线。

## 核心代码

        int count = 0, start = 0;
        
        for (int i = 0; i < tmp.size(); i++){
            if (tmp.get(i).type == 0) count++;
            else {
                if (count == 2) result.add(new Interval(start, tmp.get(i).time));
                count--;
            }
            if (count == 2) start = tmp.get(i).time;
        }



