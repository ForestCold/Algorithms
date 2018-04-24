> Given an array of n integer, and a moving window(size k), move the window at each iteration from the start of the array, find the median of the element inside the window at each moving. (If there are even numbers in the array, return the N/2-th number after sorting the element in the window. )
>

**Example:** 

For array [1,2,7,8,5], moving window size k = 3. return [2,7,7]

At first the window is at the start of the array like this

[ | 1,2,7 | ,8,5] , return the median 2;

then the window move one step forward.

[1, | 2,7,8 | ,5], return the median 7;

then the window move one step forward again.

[1,2, | 7,8,5 | ], return the median 7;

## 解题思路

维护两个priority queue，分别按照和mid的距离存放所有比当前mid值大大的数和所有比当前mid值小的数。每当窗口向前移动一位，先把移出去的数删除，再把移进来的数加入。
如果两个priority queue的size相差大于1，则进行balance，即从长的pq中取一个元素给短的pq。最后，如果某个pq更长，mid就是这个pq的peek，如果一样长就随便取一个。

## 核心代码
        
        // i为滑动窗口的起始位置
        for (int i = 1; i < nums.length - k + 1; i++){
            
            // 移走第i-1个数
            if (pqLarge.contains(nums[i - 1])) pqLarge.remove(nums[i - 1]);
            else pqSmall.remove(-1 * nums[i - 1]);
            
            // 加入第i + k - 1个数
            if (nums[i + k - 1] > result.get(result.size() - 1)) pqLarge.add(nums[i + k - 1]);
            else pqSmall.add(-1 * nums[i + k - 1]);
            
            // 平衡两个pq
            while (Math.abs(pqLarge.size() - pqSmall.size()) > 1){
                if (pqLarge.size() - pqSmall.size() > 1){
                    int balance = pqLarge.peek();
                    pqSmall.add(-1 * balance);
                    pqLarge.remove(balance);
                } else if (pqSmall.size() - pqLarge.size() > 1){
                    int balance = pqSmall.peek();
                    pqLarge.add(-1 * balance);
                    pqSmall.remove(balance);
                }
            }
            
            // 取得长的pq的peek
            if (pqLarge.size() > pqSmall.size()) result.add(pqLarge.peek());
            else result.add(-1 * pqSmall.peek());
            
        }


## 时间空间复杂度

O(nklogk) + S(k)

*n为数组长度, k为窗口长度*
