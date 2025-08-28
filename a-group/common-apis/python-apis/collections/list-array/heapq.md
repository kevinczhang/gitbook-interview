---
description: >-
  This module provides an implementation of the heap queue algorithm, also known
  as the priority queue algorithm.
---

# heapq

Heaps are binary trees for which every parent node has a value less than or equal to any of its children. We refer to this condition as the heap invariant.

This implementation uses arrays for which `heap[k] <= heap[2*k+1]` and `heap[k] <= heap[2*k+2]` for all _k_, counting elements from zero.&#x20;

That's an excellent question, and it shows you're thinking about more advanced data structures that are super useful for optimization in LeetCode! The `heapq` module in Python provides an implementation of the heap queue algorithm, also known as the priority queue algorithm.

A heap is a special tree-based data structure that satisfies the heap property: for a min-heap (which `heapq` implements), the value of each node is less than or equal to the value of its children. This means the smallest element is always at the root (index 0).

`heapq` functions operate on regular Python lists, treating them as heaps. This is a common pattern in Python's standard library: functions that operate on a generic data type (like a list) to give it special behavior.

Here are the most commonly used `heapq` methods/functions:

1. `heapq.heappush(heap, item)`:
   * Adds the `item` to the `heap` while maintaining the heap property.
   * _Why useful:_ To insert new elements into a priority queue.
   *   _Example:_

       Python

       ```python
       import heapq
       my_heap = []
       heapq.heappush(my_heap, 4)
       heapq.heappush(my_heap, 1)
       heapq.heappush(my_heap, 7)
       print(my_heap) # Output: [1, 4, 7] (order is maintained as a heap, smallest at index 0)
       ```
2. `heapq.heappop(heap)`:
   * Removes and returns the smallest item from the `heap`, maintaining the heap property.
   * _Why useful:_ To retrieve the highest-priority (smallest) element in a priority queue. This is the core operation for getting the 'next best' item.
   *   _Example:_

       Python

       ```python
       import heapq
       my_heap = [1, 4, 7] # Assuming this is already a heap
       smallest_item = heapq.heappop(my_heap)
       print(smallest_item) # Output: 1
       print(my_heap)       # Output: [4, 7] (or [7, 4] depending on internal heap structure, but 4 is still at index 0)
       ```
3. `heapq.heapify(x)`:
   * Transforms a regular list `x` into a heap, _in-place_. This is efficient (O(N) time complexity).
   * _Why useful:_ If you have an existing list of elements and want to turn it into a heap quickly.
   *   _Example:_

       Python

       ```python
       import heapq
       my_list = [7, 4, 1, 9, 2]
       heapq.heapify(my_list)
       print(my_list) # Output: [1, 2, 7, 9, 4] (smallest is at index 0)
       ```
4. `heapq.heappushpop(heap, item)`:
   * Pushes `item` onto the heap, then pops and returns the smallest item from the heap. This is often more efficient than separate push and pop calls.
   * _Why useful:_ When you want to replace the smallest element with a new element, e.g., in a fixed-size heap for finding Kth largest elements.
5. `heapq.heapreplace(heap, item)`:
   * Pops and returns the smallest item from the heap, then pushes the new `item`. This assumes the heap is non-empty.
   * _Why useful:_ Similar to `heappushpop`, but the order of operations is different.

When to use `heapq` in LeetCode:

* Priority Queues: Anytime a problem involves "processing the smallest/largest item next" or "getting the Kth smallest/largest element."
* Finding K-th Smallest/Largest Elements: Especially useful for maintaining a min-heap of size K for largest elements (or max-heap for smallest).
* Dijkstra's Algorithm, Prim's Algorithm: Graph algorithms that rely on efficiently retrieving the minimum edge/node.

