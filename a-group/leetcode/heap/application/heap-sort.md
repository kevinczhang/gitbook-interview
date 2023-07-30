# Heap Sort

**Heap Sort** sorts a group of unordered elements using the Heap data structure.

The sorting algorithm using a **Min Heap** is as follows:

1. Heapify all elements into a Min Heap.
2. Record and delete the top element.
3. Put the top element into an array T that stores all sorted elements. Now, the Heap will remain a Min Heap.
4. Repeat steps 2 and 3 until the Heap is empty. The array T will contain all elements sorted in ascending order.

The sorting algorithm using a **Max Heap** is as follows:

1. Heapify all elements into a Max Heap.
2. Record and delete the top element.
3. Put the top element into an array T that stores all sorted elements. Now, the Heap will remain a Max Heap.
4. Repeat steps 2 and 3 until the Heap is empty. The array T will contain all elements sorted in descending order.

**Complexity Analysis:**

Let NN be the total number of elements.

Time complexity: O(N \log N)O(NlogN)

Space complexity: O(N)O(N)
