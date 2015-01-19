# Partition List
##### Problem
Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,
Given `1->4->3->2->5->2` and `x = 3`,
return `1->2->2->4->3->5`.
##### Best Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
  # @param head, a ListNode
  # @param x, an integer
  # @return a ListNode
  def partition(self, head, x):
    dummyRight = ListNode(0)
    dummyLeft = ListNode(0)

    left,right = dummyLeft,dummyRight
    while head != None:
      if head.val < x:
        left.next = head
        left = head
      else:
        right.next = head
        right = head
        head = head.next
        right.next = None
        left.next = dummyRight.next
    return dummyLeft.next
```
##### Note
1. Two Pointers and Dummy Heads
    * Time Complexity:$$O(n)$$
    * Method
        * Create two dummy heads as head for left and right part
        * Loop through list to connect node to left or right part
        * Every node's next is changed only after `head` move to its next
        * Quite brilliant
