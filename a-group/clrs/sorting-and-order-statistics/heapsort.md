# Heapsort

## Heap

The (binary) heap data structure is an **array object** that we can view as a nearly complete **binary tree**. The tree is completely filled on all levels except possibly the lowest, which is filled from the left up to a point.

An array _A_ that represents a heap is an object with two attributes:

* A.length, which (as usual) gives the number of elements in the array
* A.heap-size, which represents how many elements in the heap are stored within array A.

That is may only the elements where 0 \~ A.heap-size are valid elements of the heap.

The root of the tree is A\[0], and given the index i of a node, we can easily compute the indices of its parent, left child, and right child:

* PARENT index of node i : (i -1)/2
* LEFT node index of node i: 2(i+1) - 1
* RIGHT node index of node i: 2(i+1)

### Heap build algorithm

```bash
// Time complexity O(n)
// A[n/2 + 1..n] are all leaves of the tree
A.heap-size = A.length
for i = A.length/2 to 1
    MAX-HEAPIFY(A, i)
    
// Time complexity O(h)    
MAX-HEAPIFY(A, i):
l = Left(i)
r = right(i)
largest = i
if l <= A.heap-size and A[l] > A[largest]
    largest = l;
if r <= A.heap-size and A[r] > A[largest]
    largest = r;
if (largest != i)
    exchange A[i] with A[largest]
    MAX-HEAPIFY(A, largest) 
```

### Heap sort algorithm

```bash
// Time complexity O(nlgn)
BUILD-MAX-HEAP(A)
for i = A.length to 2
    exchange A[1] with A[i]
    A.heap-szie = A.heap-size - 1
    MAX-HEAPIFY(A, i)
```

## Priority Queue

A **priority queue** is a data structure for maintaining a set _S_ of elements, each with an associated value called a **key**.

A max-priority queue supports the following operations:&#x20;

* INSERT(S, x): inserts the element x into the set S, which is equivalent to the operation S = S U {x}.&#x20;
* MAXIMUM(S): returns the element of S with the largest key.&#x20;
* EXTRACT-MAX(S): removes and returns the element of S with the largest key.&#x20;
* INCREASE-KEY(S,x, k): increases the value of element x’s key to the new value k, which is assumed to be at least as large as x’s current key value.

#### HEAP-MAXIMUM(A)

```bash
return A[1]
```

#### HEAP-EXTRACT-MAX(A)

Time complexity O(lgn)

```bash
if A.heap-size < 1
    error “heap underflow”
max = A[1]
A[1] = A[A.heap-size]
A.heap-size = A.heap-size - 1
MAX-HEAPIFY(A, 1)
return max
```

#### HEAP-INCREASE-KEY(A, i, key)

```bash
if key < A[i]
    error “new key is smaller than current key”
A[i] = key
while i > 1 and A[PARENT(i)] < A[i]
    exchange A[i] with A[PARENT(i)]
    i = PARENT(i)
```

#### MAX-HEAP-INSERT(A, key)

```bash
A.heap-size = A.heap-size + 1
A[A.heap-size] = -infinite
HEAP-INCREASE-KEY(A, A.heap-size, key)
```
