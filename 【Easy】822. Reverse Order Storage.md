> Give a linked list, and store the values of linked list in reverse order into an array.
>
> **Notice**
> + You can not change the structure of the original linked list.

**Example:** 

Given 1 -> 2 -> 3 -> null, return [3,2,1].

## 解题思路

略。

## 核心代码

        while (h != null) {
            stack.push(h.val);
            h = h.next;
        }
        
        while (stack.size() > 0){
            result.add(stack.pop());
        }

## 时间空间复杂度

O(n) + S(n)

