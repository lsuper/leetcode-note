# Sort List
##### Problem
Sort a linked list in $$O(n log n)$$ time using constant space complexity.

Note: Methods I use here is not constant space complexity
##### Best Solution: Merge Sort
```python
# Definition for singly-linked list.
#class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    # @param head, a ListNode
    # @return a ListNode
    def sortList(self, head):
        if head == None or head.next == None:
            return head
        dummyHead = ListNode(0)
        dummyHead.next = head
        #add a dummy node to the head, makes the midNode = (headIndex + endIndex)/2
        #If list is longer than 1 elements, left half and right half will or less than the whole list size
        midNode = self.findMidNode(dummyHead)
        right = midNode.next
        midNode.next = None
        left = self.sortList(head)
        right = self.sortList(right)

        node = dummyHead
        while left != None and right != None:
            if left.val <= right.val:
                node.next = left
                left = left.next
            else:
                node.next = right
                right = right.next
            node = node.next

        if left != None:
            node.next = left
        else:
            node.next = right

        return dummyHead.next


    def findMidNode(self, head):
        slow = fast = head
        while fast != None and fast.next != None:
            slow = slow.next
            fast = fast.next.next

        return slow

```
##### Best Solution: Quick Sort
```python
# Definition for singly-linked list.
#class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    # @param head, a ListNode
    # @return a ListNode
    def sortList(self, head):
        return self.quickSort(head)[0]

    def quickSort(self, head):
        #quick sort
        if head == None or head.next == None:
            return head, head
        #have to divide in three parts, otherwise TLE
        left, mid, midEnd, right = self.partition(head, head.val)
        left, leftLast = self.quickSort(left)
        midEnd.next, rightLast = self.quickSort(right)
        if left != None:
            leftLast.next = mid
            if rightLast != None:
                return left, rightLast
            else:
                return left, midEnd
            else:
                if rightLast != None:
                    return mid, rightLast
                else:
                    return mid, midEnd

    def partition(self, head, val):
        dummyRight = ListNode(0)
        dummyLeft = ListNode(0)
        dummyMid = ListNode(0)
        left, right, mid = dummyLeft, dummyRight, dummyMid
        while head != None:
            if head.val < val:
                left.next = head
                left = left.next
            elif head.val > val:
                right.next = head
                right = right.next
            else:
                mid.next = head
                mid = mid.next
                head = head.next
        left.next = None
        right.next = None
        mid.next = None
        return dummyLeft.next, dummyMid.next, mid, dummyRight.next
```
##### Note
1. Merge Sort
    * Time Complexity: $$O(n\log n)$$
    * Space Complexity: $$O(\log n)$$ stack space
    * Method
        * Use two pointers to find the `midNode`. Make sure every round size of left and right halves from original list. Refer to inline comment
        * The rest is just common approach to merge two sorted list
2. Quick Sort
    * Time Complexity: $$O(n\log n)$$
    * Space Complexity: $$O(\log n)$$ stack space
    * Method
        * Use `partition list` approach to do list partition, be sure to disconnect left, mid, right part in `partition` method
        * Partition list into 3 parts, less, equal and greater than pivot node
3. Constant Space
    * To achieve constant space, we need to do a bottom-up implementation of **merge sort**
    * Use a loop to do merge or quick sort for a group of 1, 2, 4, ..., n/2 nodes each round.
    * Inside the loop do the merge each group with its neighbor group.
    * Quick Sort cannot be implemented in bottom-up way.
