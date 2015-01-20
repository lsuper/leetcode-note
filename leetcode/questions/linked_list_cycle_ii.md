#Linked List Cycle
##### Problem
Given a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

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
    # @return a list node
    def detectCycle(self, head):
        if head == None or head.next == None or head.next.next == None:
            return None

        slow = fast = head
        while fast.next and fast.next.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                break
        if slow == fast:
            slow = head
            while slow != fast:
                slow = slow.next
                fast = fast.next
            return slow
        else:
            return None
```
##### Note
1. Two pointers
    * Time Complexity: O(n)
    * Method
        * Fast and slow pointers will eventually meet if there is a cycle
        * After they meet, move one pointer to the head of linked list
        * Then two pointers move at the same speed on the linked list one by one
        * The next meet point will be the cycle start
    * Just be careful about relationship of corner cases and how you detect cycle in while loop.
