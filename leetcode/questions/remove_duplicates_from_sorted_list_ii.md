# Remove Duplicates from Sorted List 
##### Problem
Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

For example,
Given `1->2->3->3->4->4->5`, return `1->2->5`.  
Given `1->1->1->2->3`, return `2->3`.
##### Best Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    # @param head, a ListNode
    # @return a ListNode
    def deleteDuplicates(self, head):
        node = head
        while node:
            if node.next and node.next.val == node.val:
                node.next = node.next.next
            else:
                node = node.next
        return head
```
##### Note
1. Keep the first, move to next if it is not a duplicate.
    * Time Complexity: $$O(n)$$
        * Method: