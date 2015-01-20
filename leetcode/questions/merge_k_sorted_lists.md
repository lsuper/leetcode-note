# Template
##### Problem
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.
##### Best Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    # @param a list of ListNode
    # @return a ListNode
    def mergeKLists(self, lists):
        dummyHead = ListNode(0)
        pre = dummyHead
        hq = [(node.val, node) for node in lists if node]
        heapq.heapify(hq)
        while len(hq) > 1:
            val, node = heapq.heappop(hq)
            pre.next = node
            pre = pre.next
            node = node.next
            if node:
                heapq.heappush(hq, (node.val, node))
        if len(hq) == 1:
            pre.next = hq[0][1]
        return dummyHead.next
```
##### Note
1. Heap
    * Time Complexity: $$O(nlogn)$$
    * Method
        * Build a heap to store the first nodes of each list
        * Get out the minimum
        * Push into the minimum's next node
2. `heapq` is a core python package. Common methods include `heappush`, `heappop`, `heapify`. It just makes a ordinary list sorted as a minHeap.
Each element can be a tuple/list and the first element of tuple/list is used for comparison
