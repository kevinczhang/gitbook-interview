# Set Interface

## Overview

```java
public interface Collection<E> extends Iterable<E>
```

1. SortedSet is a subInterface of Set Interface. TreeSet implemented SortedSet.
2. HashSet and LinkedHashSet are common implementations of Set Interface.

## SortedSet

### Commonly used methods

1. &#x20;[`first`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedSet.html#first--)`()`Returns the first (lowest) element currently in this set.
2. &#x20;[`headSet`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedSet.html#headSet-E-)`(`[`E`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedSet.html) `toElement)`Returns a view of the portion of this set whose elements are strictly less than toElement.
3. &#x20;[`last`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedSet.html#last--)`()`Returns the last (highest) element currently in this set.
4. &#x20;[`subSet`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedSet.html#subSet-E-E-)`(`[`E`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedSet.html) `fromElement,` [`E`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedSet.html) `toElement)`Returns a view of the portion of this set whose elements range from fromElement, inclusive, to toElement, exclusive.
5. &#x20;[`tailSet`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedSet.html#tailSet-E-)`(`[`E`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedSet.html) `fromElement)`Returns a view of the portion of this set whose elements are greater than or equal to fromElement.

## TreeSet

#### Constructor Summary

1. &#x20;[`TreeSet`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html#TreeSet--)`()`Constructs a new, empty tree set, sorted according to the natural ordering of its elements.
2. &#x20;[`TreeSet`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html#TreeSet-java.util.Collection-)`(`[`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html)`<? extends` [`E`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html)`> c)`Constructs a new tree set containing the elements in the specified collection, sorted according to the natural ordering of its elements.
3. &#x20;[`TreeSet`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html#TreeSet-java.util.Comparator-)`(`[`Comparator`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)`<? super` [`E`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html)`> comparator)`Constructs a new, empty tree set, sorted according to the specified comparator.

#### Method Summary

1. &#x20;[`ceiling`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html#ceiling-E-)`(`[`E`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html) `e)`Returns the least element in this set greater than or equal to the given element, or `null` if there is no such element.
2. &#x20;[`floor`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html#floor-E-)`(`[`E`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html) `e)`Returns the greatest element in this set less than or equal to the given element, or `null` if there is no such element.
3. &#x20;[`first`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html#first--)`()`Returns the first (lowest) element currently in this set.
4. &#x20;[`last`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html#last--)`()`Returns the last (highest) element currently in this set.
5. &#x20;[`pollFirst`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html#pollFirst--)`()`Retrieves and removes the first (lowest) element, or returns `null` if this set is empty.
6. &#x20;[`pollLast`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html#pollLast--)`()`Retrieves and removes the last (highest) element, or returns `null` if this set is empty.
7. &#x20;[`descendingIterator`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html#descendingIterator--)`()`Returns an iterator over the elements in this set in descending order.
