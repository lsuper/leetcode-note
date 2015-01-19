# Sorting
#### Common Sorting Algorithms

* **Bubble Sort**
    * Stable
    * Time: $$O(n^2)$$
    * Space: $$O(1)$$
    * Each round Move the largest to the end.
* **Insertion Sort**
    * Stable
    * Time: $$O(n^2)$$
    * Space: $$O(1)$$
    * Maintain the sorted part and shrink the unsorted part
    * Insert each number to its sorted position
* **Selection Sort**
    * Stable: move instead of swap; Non-stable: because of swap
    * Time: $$O(n^2)$$
    * Space: $$O(1)$$
    * Put the smallest number to the end of sorted part
* **Merge Sort**
    * Stable
    * Time: $$O(n\log n)$$
    * Space: recursive $$O(\log n)$$, $$O(n)$$worst case; in-place $$O(1)$$ for list
    * Divide the list into halves
    * Recursively merge sort each half
    * Merge them
* **Quick Sort**
    * Non-stable
    * Time: $$O(n\log n)$$, $$O(n)$$worst case
    * Space: $$O(n \log n)$$; can be $$O(1)$$ for list
    * Split the list based on a pivot number, first part < pivot <= second part
    * Recursively quick sort for first and second parts
* **Heap Sort**
    * Non-stable
    * Time: $$O(n\log n)$$
    * Space: $$O(1)$$
    * Build a heap (minimum or maximum) first
    * Move the root to sorted part
    * Move the new root (which is the last of previous heap tree) to correct position in heap
    * Heap is often placed in an array with the layout of a complete binary tree. If `i` is the index of current node
    ```
    parentIndex = floor((i-1)/2)
    leftChildIndex = 2*i + 1
    rightChildIndex = 2*i + 2
    ```
* **Distribution Sort**
    * This allows **external sorting** of data too large to fit into a single computer's memory.
    * **Counting Sort**
        * Stable
        * Time: $$O(n+r)$$
        * Space: $$O(n+r)$$, $$r$$ is the range of input numbers
        ```python
        # variables:
        #    input -- the array of items to be sorted; key(x) returns the key for item x
        #    n -- the length of the input
        #    k -- a number such that all keys are in the range 0..k-1
        #    count -- an array of numbers, with indexes 0..k-1, initially all zero
        #    output -- an array of items, with indexes 0..n-1
        #    x -- an individual input item, used within the algorithm
        #    total, oldCount, i -- numbers used within the algorithm

        # calculate the histogram of key frequencies:
        for x in input:
            count[key(x)] += 1

        # calculate the starting index for each key:
        total = 0
        for i in range(k):   # i = 0, 1, ... k-1
            oldCount = count[i]
            count[i] = total
            total += oldCount

        # copy to output array, preserving order of inputs with equal keys:
        for x in input:
            output[count[key(x)]] = x
            count[key(x)] += 1

        return output
        ```
    * **Bucket Sort**
        * Depends on the sorting algorithm
        * Time: $$O(n+r)$$, $$r$$ is number of buckets
        * Space: $$O(n+r)$$
        * Distribute numbers in to different buckets
        * Sort each bucket with any sorting algorithm
        * Output numbers within all the buckets in order
    * **Radix Sort**
        * Can be stable
        * Time: LSD $$O((n+k) * d)$$
        * Sort from either least significant digit (LSD) or most significant digit (MSD)
        * LSD requires stable sorting, while MSD does not
* Implementation for both linked list and array
* Analysis
    * Time Complexity
    * Space Complexity: in-place or not
    * Stable or not

#### Questions
1.[Sort List](/leetcode-note/content/leetcode/questions/sort_list.html)
