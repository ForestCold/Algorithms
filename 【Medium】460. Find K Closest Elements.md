> Given a target number, a non-negative integer target and an integer array A sorted in ascending order, find the k closest numbers to target in A, sorted in ascending order by the difference between the number and target. Otherwise, sorted in ascending order by number if the difference is same.
>

**Example:** 

Given A = [1, 2, 3], target = 2 and k = 3, return [2, 1, 3].

Given A = [1, 4, 6, 8], target = 3 and k = 3, return [4, 1, 6].

## 解题思路

先用二分法找到最接近target的数字，然后在这个数字两边放两个指针，依次向外扩张的同时把最接近target的数存入结果中。

## 核心代码

找到最接近的数字年后依次放入结果数组：

        while (count < k){
            if (left < 0 || (right < A.length && Math.abs(A[right] - target) < Math.abs(A[left] - target))){
                result[count] = A[right];
                right++;
            } else if (right >= A.length || (left >= 0 && Math.abs(A[right] - target) >= Math.abs(A[left] - target))){
                result[count] = A[left];
                left--;
            } 
            count++;
        }

## 时间空间复杂度

O(Max(logn, k)) + S(1)

*n为数组长度*
