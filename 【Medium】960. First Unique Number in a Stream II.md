> We need to implement a data structure named DataStream. There are two methods required to be implemented:
> 
> 1 void add(number) // add a new number
>
> 2 int firstUnique() // return first unique number
>
> **Notice**
>
> You can assume that there must be at least one unique number in the stream when calling the firstUnique.
>

**Example:** 

    add(1)
    add(2)
    firstUnique() => 1
    add(1)
    firstUnique() => 2

## 解题思路

记录上一次获取的first unique值，下一次获取时不再考虑这个值之前的元素。

## 核心代码

        for (int i = pointer; i < list.size(); i++) {
            if (map.get(list.get(i)) == 1) {
                pointer = i;
                break;
            }
        }

## 时间空间复杂度

O(n) + S(n)
