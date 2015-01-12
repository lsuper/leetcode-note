# Remove Duplicates from Sorted List II
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
    #ninechapter method
    def deleteDuplicates(self, head):
        dummyNode = ListNode(0)
        dummyNode.next = head
        node = dummyNode
        while node.next and node.next.next:
            if node.next.val == node.next.next.val:
                curVal = node.next.val
                while node.next and node.next.val == curVal:
                    node.next = node.next.next
            else:
                node = node.next
        return dummyNode.next
```
##### Note
1. Check next two nodes
    * Time Complexity: $$O(n)$$
    * Method
        * Create a dummy node before head. `node` is the last unique node, `node` is connected to the next node with a new value. If there is less than two nodes after `node`, we can return the head `dummyNode.next`. Otherwise, if `node.next.val == node.next.next.val`, we know `node.next` is a new unique node, we move `node` to `node.next`. If `node.next.val != node.next.next.val`, that means `node.next` is also a duplicate, we move `node.next` until it points to the next value or reach the end of list.
        * The trick part is check next two nodes together.