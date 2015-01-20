# Template
##### Problem
Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

##### Best Solution
```python
# Definition for a  binary tree node
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
#
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    # @param head, a list node
    # @return a tree node
    def sortedListToBST(self, head):
        self.lst = []
        while head:
            self.lst.append(head.val)
            head = head.next
        return self.helper(0, len(self.lst) - 1)

    def helper(self, start, end):
        if start > end:
            return None
        mid = start + (end - start)/2
        root = TreeNode(self.lst[mid])
        root.right = self.helper(mid + 1, end)
        root.left = self.helper(start, mid - 1)
        return root
```
##### Note
1. Transform to list and build a BST
    * Time Complexity: $$O(n)$$
    * Method
