> Give an array, all the numbers appear twice except one number which appears once and all the numbers which appear twice are next to each other. Find the number which appears once.
>
> **Notice:** 
>+ 1 <= nums.length < 10^4
>+ In order to limit the time complexity of the program, your program will run 10^5 times.

**Example:** 

Given nums = [3,3,2,2,4,5,5], return 4.

    Explanation:
    4 appears only once.
    
Given nums = [2,1,1,3,3], return 2.

    Explanation:
    2 appears only once.

## 解题思路

用二分法，当取mid的时候，array被分成了左右两个子array，此时判断mid与它左边的值是否相等。
若两个子array的长度为奇数且mid与它左边的值相等，证明单个的数出现在mid的右边，反之则出现在mid的左边。
若两个子array的长度为偶数且mid与它左边的值相等，证明单个的数出现在mid的左边，反之则出现在mid的右边。
在更新start和end时要注意不能把一对相等的数分开，并且一定要包含可能的单个的数。

## 核心代码

        while (start + 1 < end){
            int mid = start + (end - start) / 2;
            if ((mid - start) % 2 == 1){
                if (mid - 1 >= 0 && nums[mid] == nums[mid - 1]){
                    start = mid + 1;
                } else {
                    end = mid;
                }
            } else {
                if (mid - 1 >= 0 && nums[mid] == nums[mid - 1]){
                    end = mid - 2;
                } else {
                    start = mid;
                }
            }
        }


## 时间空间复杂度

O(logn) + S(1)
*n为数组长度*
