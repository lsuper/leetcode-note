# Reverse Linked List II
##### Problem
Reverse a linked list from position m to n. Do it in-place and in one-pass.

For example:  
Given `1->2->3->4->5->NULL`, `m = 2` and `n = 4`,

return `1->4->3->2->5->NULL`.

Note:
Given `m, n` satisfy the following condition:
`1 ≤ m ≤ n ≤ length of list`.
##### Best Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    # @param head, a ListNode
    # @param m, an integer
    # @param n, an integer
    # @return a ListNode
    def reverseBetween(self, head, m, n):
        if m == n:
            return head
        dummyHead = ListNode(0)
        dummyHead.next = head
        node1 = node2 = dummyHead
        preReverseNode = postReverseNode = None
        while m > 0:
            if m == 1:
                preReverseNode = node1
            m -= 1
            node1 = node1.next

        while n > 0:
            n -= 1
            node2 = node2.next

        postReverseNode = node2.next
        preReverseNode.next = node2

        preNode = postReverseNode
        while node1 != postReverseNode:
            next = node1.next
            node1.next = preNode
            preNode = node1
            node1 = next

        return dummyHead.next

```
##### Note
1. Dummy head
    * Time Complexity: $$O(n)$$
    * Method
        * Since the head node may be removed, by adding a dummy head, we can simplify the whole reversing process.
