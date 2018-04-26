> Given a sorted integer array where the range of elements are in the inclusive range [lower, upper], return its missing ranges.
>

**Example:** 

Given nums = [0, 1, 3, 50, 75], lower = 0 and upper = 99
return ["2", "4->49", "51->74", "76->99"].

## 解题思路

这题的难点在于corner case的考虑，即Integer.MAX_VALUE不能加1，Integer.MIN_VALUE不能减1。

## 核心代码
        
        // 从start到第一个元素
        if (start > Integer.MIN_VALUE + 1 && lower < start - 1) result.add("" + lower + "->" + (start - 1));
        else if (lower < start) result.add("" + lower);
        
        // 所有元素的缝隙
        for (int i = 1; i < nums.length; i++){
            if (start != Integer.MAX_VALUE && nums[i] != Integer.MIN_VALUE && nums[i] > start + 1) {
                if (start + 1 == nums[i] - 1) result.add("" + (start + 1));
                else result.add("" + (start + 1) + "->" + (nums[i] - 1));
            }
            start = nums[i];
        }
        
        // 从最后一个元素到end
        if (upper >= Integer.MIN_VALUE + 1 && start < upper - 1) result.add("" + (start + 1) + "->" + upper);
        else if (upper >= Integer.MIN_VALUE && start < upper) result.add("" + (upper));

## 时间空间复杂度

O(n) + S(1)

