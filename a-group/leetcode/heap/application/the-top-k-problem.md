# The Top K Problem



#### The Top K Problem - Approach 1 <a href="#the-top-k-problem-approach-1" id="the-top-k-problem-approach-1"></a>

Use the Heap data structure to obtain Top K’s largest or smallest elements.

Solution of the Top K largest elements:

1. Construct a Max Heap.
2. Add all elements into the Max Heap.
3. Traversing and deleting the top element (using pop() or poll() for instance), and store the value into the result array T.
4. Repeat step 3 until we have removed the K largest elements.

Solution of the Top K smallest elements:

1. Construct a Min Heap.
2. Add all elements into the Min Heap.
3. Traversing and deleting the top element (using pop() or poll() for instance), and store the value into the result array T.
4. Repeat step 3 until we have removed the K smallest elements.

**Complexity Analysis:**

Time complexity: O(K \log N + N)O(KlogN+N)

* Steps one and two require us to construct a Max Heap which requires O(N)O(N) time using the previously discussed heapify method. Each element removed from the heap requires O(\log N)O(logN) time; this process is repeated KK times. Thus the total time complexity is O(K \log N + N)O(KlogN+N).

Space complexity: O(N)O(N)

* After step 2, the heap will store all NN elements.

***

&#x20;

***

#### The Top K Problem - Approach 2 <a href="#the-top-k-problem-approach-2" id="the-top-k-problem-approach-2"></a>

Use the **Heap** data structure to obtain Top K’s largest or smallest elements.

Solution of the Top K largest elements:

1. Construct a Min Heap with size K.
2. Add elements to the Min Heap one by one.
3. When there are K elements in the “Min Heap”, compare the current element with the top element of the Heap:
4. If the current element is no larger than the top element of the Heap, drop it and - proceed to the next element.
5. If the current element is larger than the Heap’s top element, delete the Heap’s top element, and add the current element to the Min Heap.
6. Repeat Steps 2 and 3 until all elements have been iterated.

Now the K elements in the Min Heap are the K largest elements.

Solution of the Top K smallest elements:

1. Construct a Max Heap with size K.
2. Add elements to the Max Heap one by one.
3. When there are K elements in the “Max Heap”, compare the current element with the top element of the Heap:
4. If the current element is no smaller than the top element of the Heap, drop it and proceed to the next element.
5. If the current element is smaller than the top element of the Heap, delete the top element of the Heap, and add the current element to the Max Heap.
6. Repeat Steps 2 and 3 until all elements have been iterated.

Now the K elements in the Max Heap are the K smallest elements.

**Complexity Analysis:**

Time complexity: O(N \log K)O(NlogK)

* Steps one and two will require O(K \log K)O(KlogK) time if the elements are added one by one to the heap, however using the heapify method, these two steps could be accomplished in O(K)O(K) time. Steps 3 and 4 will require O(\log K)O(logK) time each time an element must be replaced in the heap. In the worst-case scenario, this will be done N - KN−K times. Thus the total time complexity is O((N - K) \log K + K \log K)O((N−K)logK+KlogK) which simplifies to O(N \log K)O(NlogK).

Space complexity: O(K)O(K)

* The heap will contain at most KK elements at any given time.
