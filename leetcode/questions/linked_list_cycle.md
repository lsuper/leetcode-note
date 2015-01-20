#Linked List Cycle
##### Problem
Given a linked list, determine if it has a cycle in it.


Follow up:

Can you solve it without using extra space?
##### Best Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    # @param head, a ListNode
    # @return a boolean
    def hasCycle(self, head):
        if head == None:
            return False
        slow = fast = head
        while fast.next and fast.next.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True
        return False
```
##### Note
1. Two pointers
    * Time Complexity: O(n)
    * Method
        * Fast and slow pointers will eventually meet if there is a cycle
