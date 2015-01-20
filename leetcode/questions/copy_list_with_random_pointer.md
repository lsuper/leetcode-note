# Copy List with Random Pointer
##### Problem
A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

##### Best Solution
```python
# Definition for singly-linked list with a random pointer.
# class RandomListNode:
#     def __init__(self, x):
#         self.label = x
#         self.next = None
#         self.random = None

class Solution:
    # @param head, a RandomListNode
    # @return a RandomListNode
    def copyRandomList(self, head):
        table = {None: None}
        dummyHead = RandomListNode(0)
        pre = dummyHead
        node = head
        while node:
            table[node] = RandomListNode(node.label)
            pre.next = table[node]
            node = node.next
            pre = pre.next

        node = head
        while node:
            table[node].random = table[node.random]
            node = node.next
        return dummyHead.next
```
##### Note
1. Hash table
    * Time Complexity:
    * Method
        * First loop for building list
        * Second loop for connecting random pointers
        * Use a hash table to map between old nodes to new nodes
