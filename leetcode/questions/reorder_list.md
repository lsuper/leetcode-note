# Reorder List
##### Problem
Given a singly linked list L: `L0→L1→…→Ln-1→Ln`,  
reorder it to: `L0→Ln→L1→Ln-1→L2→Ln-2→…`

You must do this in-place without altering the nodes' values.

For example,
Given ``{1,2,3,4}``, reorder it to ``{1,4,2,3}``.
##### Best Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
class Solution:
    # @param head, a ListNode
    # @return nothing
    def reorderList(self, head):
        if head == None or head.next == None:
            return head
        left, right = self.breakAtMid(head)
        right = self.reverse(right)
        return self.merge(left, right)

    def breakAtMid(self, head):
        slow, fast = head, head.next
        while fast.next and fast.next.next:
            slow = slow.next
            fast = fast.next.next
        right = slow.next
        slow.next = None
        return head, right

    def reverse(self, head):
        pre = None
        cur = head
        while cur:
            next = cur.next
            cur.next = pre
            pre = cur
            cur = next
        return pre

    def merge(self, left, right):
        dummyHead = ListNode(0)
        head = dummyHead
        flag = True
        while left and right:
            if flag:
                head.next = left
                left = left.next
            else:
                head.next = right
                right = right.next
            head = head.next
            flag = not flag

        if left == None:
            head.next = right

        if right == None:
            head.next = left

        return dummyHead.next
```
##### Note
1. Break, Reverse, Merge
    * Time Complexity: $$O(n)$$
    * Method
        * Break from the mid node (`breakAtMid` breaks even size list at `(start + end)/2`, for odd size list: `(start + end)/2 - 1)`
        * Reverse the right half
        * Merge two lists
