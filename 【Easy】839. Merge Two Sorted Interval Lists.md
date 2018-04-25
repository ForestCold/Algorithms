> Merge two sorted (ascending) lists of interval and return it as a new sorted list. The new sorted list should be made by splicing together the intervals of the two lists and sorted in ascending order.
>
> **Notice:** 
> + The intervals in the given list do not overlap.
> + The intervals in different lists may overlap.

**Example:** 

Given list1 = [(1,2),(3,4)] and list2 = [(2,3),(5,6)], return [(1,4),(5,6)].

## 解题思路

把start和end都扔到一个list里进行排序，如果time相等则start排在前面。遍历list，维护一个变量，遇到start则加1，遇到end则减1，等于0时将start和当前的end加入结果。

## 核心代码
  
    // 重载
    class Point implements Comparable<Point>{
        int time, type;
        Point(int ti, int ty){
            this.time = ti;
            this.type = ty;
        }
        
        @Override
        public int compareTo(Point p){
            if (this.time != p.time)
                return (int)(this.time - p.time);
            else return (int)(p.type - this.type);
        }
    }
    
     // 扫描
     int balance = 0, start = 0;

     for (int i = 0; i < tmp.size(); i++){
         if (tmp.get(i).type == 1){
              if (balance == 0) start = tmp.get(i).time;
              balance++;
         } 
         else balance--;
         if (balance == 0){
              result.add(new Interval(start, tmp.get(i).time));
         }
      }
    
## 时间空间复杂度

O(n) + S(n)



