# Queue Interface

## Overview

```java
public interface Queue<E> extends Collection<E>
```

1. Deque Interface (public interface Deque\<E> extends Queue\<E>). Implementation is .
2. &#x20;[ArrayDeque](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayDeque.html) and  [LinkedList](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html) are the most commonly used implementations of Deque.
3. &#x20;[LinkedList](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html) and  [PriorityQueue](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html) are the most commonly used implementations of Queue.

### Common methods

1. &#x20;[`offer`](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html#offer-E-)`(`[`E`](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html) `e);`Inserts the specified element into this queue if it is possible to do so immediately without violating capacity restrictions.
2. &#x20;[`peek`](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html#peek--)`();`Retrieves, but does not remove, the head of this queue, or returns `null` if this queue is empty.
3. &#x20;[`poll`](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html#poll--)`();`Retrieves and removes the head of this queue, or returns `null` if this queue is empty.

## Deque

ArrayDeque not allow null but LinkedList allow.

### Methods

1. &#x20;[`offerFirst`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html#offerFirst-E-)`(`[`E`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html) `e)`Inserts the specified element at the front of this deque unless it would violate capacity restrictions.
2. &#x20;[`offerLast`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html#offerLast-E-)`(`[`E`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html) `e)`Inserts the specified element at the end of this deque unless it would violate capacity restrictions.
3. &#x20;[`peekFirst`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html#peekFirst--)`()`Retrieves, but does not remove, the first element of this deque, or returns `null` if this deque is empty.
4. &#x20;[`peekLast`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html#peekLast--)`()`Retrieves, but does not remove, the last element of this deque, or returns `null` if this deque is empty.
5. &#x20;[`pollFirst`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html#pollFirst--)`()`Retrieves and removes the first element of this deque, or returns `null` if this deque is empty.
6. &#x20;[`pollLast`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html#pollLast--)`()`Retrieves and removes the last element of this deque, or returns `null` if this deque is empty.

## PriorityQueue

&#x20;The _head_ of this queue is the _least_ element with respect to the specified ordering.

### Constructor Summary

1. &#x20;[`PriorityQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html#PriorityQueue--)`()`Creates a `PriorityQueue` with the default initial capacity (11) that orders its elements according to their [natural ordering](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html).
2. &#x20;[`PriorityQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html#PriorityQueue-java.util.Collection-)`(`[`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html)`<? extends` [`E`](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html)`> c)`Creates a `PriorityQueue` containing the elements in the specified collection.
3. &#x20;[`PriorityQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html#PriorityQueue-java.util.Comparator-)`(`[`Comparator`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)`<? super` [`E`](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html)`> comparator)`Creates a `PriorityQueue` with the default initial capacity and whose elements are ordered according to the specified comparator.

### Method Summary

1. &#x20;[`offer`](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html#offer-E-)`(`[`E`](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html) `e)`Inserts the specified element into this priority queue.
2. &#x20;[`peek`](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html#peek--)`()`Retrieves, but does not remove, the head of this queue, or returns `null` if this queue is empty.
3. &#x20;[`poll`](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html#poll--)`()`Retrieves and removes the head of this queue, or returns `null` if this queue is empty.
