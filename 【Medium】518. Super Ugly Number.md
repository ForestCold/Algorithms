> Write a program to find the nth super ugly number.
>
> Super ugly numbers are positive numbers whose all prime factors are in the given prime list primes of size k. For example, [1, 2, 4, 7, 8, 13, 14, 16, 19, 26, 28, 32] is the sequence of the first 12 super ugly numbers given primes = [2, 7, 13, 19] of size 4.
>
> **Notice:** 
> + 1 is a super ugly number for any given primes.
> + The given numbers in primes are in ascending order.
> + 0 < k ≤ 100, 0 < n ≤ 10^6, 0 < primes[i] < 1000

**Example:** 

Given n = 6, primes = [2, 7, 13, 19] return 13

## 解题思路

测试数据并不是ascending order...所以代码按照随机order写。剪枝条件是当前数大于第K小的数，维护一个queue，每次把poll出来的数字乘以prime数组中的每个数
再加入队列，ascending下的理想状况是整体扫描趋势从小到大。

## 核心代码

        pq.add((long)(-1));
        
        for (int i = 0; i < primes.length; i++){
            queue.offer((long)primes[i]);
        }
        
        while (queue.size() > 0){
            long head = queue.poll();
            pq.add(-1 * head);
            for (int i = 0; i < primes.length; i++) {
                if (pq.size() > n && primes[i] * head > -1 * pq.peek()) continue;
                if (!queue.contains(primes[i] * head)) queue.offer(primes[i] * head);
            }
            while (pq.size() > n) pq.remove(pq.peek());
        }
        
## 时间空间复杂度

O(k) + S(k)

*k为prime数组长度*



