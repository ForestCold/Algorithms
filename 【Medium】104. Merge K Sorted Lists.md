> Merge k sorted linked lists and return it as one sorted list.
>
> Analyze and describe its complexity.
>

**Example:** 

Given lists:

    [
      2->4->null,
      null,
      -1->null
    ],

return -1->2->4->null.

## 解题思路

全部扔到一个Priority Queue里。

## 核心代码

        PriorityQueue<Integer> pq = new PriorityQueue<>();
        ListNode dummy = new ListNode(0);
        ListNode head = dummy;
        
        for (int i = 0; i < lists.size(); i++){
            ListNode node = lists.get(i);
            while (node != null){
                pq.add(node.val);
                node = node.next;
            }
        }
        
        while (pq.size() > 0){
            ListNode node = new ListNode(pq.peek());
            pq.remove(pq.peek());
            head.next = node;
            head = head.next;
        }
        
        return dummy.next;

## 时间空间复杂度

O(nlog(n/2)) + S(n)

*n为k个数组的总长度*


