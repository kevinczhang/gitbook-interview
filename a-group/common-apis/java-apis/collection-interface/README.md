---
description: Collection Interface and Collections Class
---

# Collection

## Collection Interface

```java
public interface Collection extends Iterable
```

### Iterable Interface

Available methods: hasNext, next, remove

```java
List<String> nameList = new ArrayList<>();
Iterator<String> itr = nameList.iterator();
while(itr.hasNext()) {
	itr.next();
	// Must call next before remove
	itr.remove();
}
```

### Collection subInterfaces and methods

1. Commonly used subInterfaces: [List](https://interviewprepspace.gitbook.io/project/\~/edit/drafts/-LUNMZGQAZaD5Ap8yYw1/common-apis/common-apis-2/collection-interface/list-interface), [Queue](https://interviewprepspace.gitbook.io/project/\~/edit/drafts/-LUNMZGQAZaD5Ap8yYw1/common-apis/common-apis-2/collection-interface/queue-interface) and Set
2. &#x20;boolean`add(E e):`Ensures that this collection contains the specified element.
3. &#x20;[`boolean addAll`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html#addAll-java.util.Collection-)`(`[`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html)`<? extends E> c):`Adds all of the elements in the specified collection to this collection.
4. &#x20;[`boolean lear`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html#clear--)`();`Removes all of the elements from this collection.
5. &#x20;[`contains`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html#contains-java.lang.Object-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) `o);`Returns true if this collection contains the specified element.
6. &#x20;[`containsAll`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html#containsAll-java.util.Collection-)`(`[`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html)`<?> c);`Returns true if this collection contains all of the elements in the specified collection.
7. &#x20;[`boolean remove`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html#remove-java.lang.Object-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) `o);`Removes a single instance of the specified element from this collection, if it is present.
8. &#x20;[`boolean removeAll`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html#removeAll-java.util.Collection-)`(`[`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html)`<?> c);`Removes all of this collection's elements that are also contained in the specified collection.
9. &#x20;[`removeIf`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html#removeIf-java.util.function.Predicate-)`(`[`Predicate`](https://docs.oracle.com/javase/8/docs/api/java/util/function/Predicate.html)`<? super` [`E`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html)`> filter);`Removes all of the elements of this collection that satisfy the given predicate.
10. &#x20;[`size`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html#size--)`();`Returns the number of elements in this collection.
11. &#x20;[Object](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)\[][`toArray`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html#toArray--)`();`Returns an array containing all of the elements in this collection.
12. &#x20;[`isEmpty`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html#isEmpty--)`();`Returns true if this collection contains no elements.

## Commonly used methods in Collections Class

1. &#x20;[`shuffle`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#shuffle-java.util.List-)`(`[`List`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html)`<?> list)`Randomly permutes the specified list using a default source of randomness.
2. &#x20;[`shuffle`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#shuffle-java.util.List-java.util.Random-)`(`[`List`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html)`<?> list,` [`Random`](https://docs.oracle.com/javase/8/docs/api/java/util/Random.html) `rnd)`Randomly permute the specified list using the specified source of randomness.
3. &#x20;[`sort`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#sort-java.util.List-)`(`[`List`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html)`<T> list)`Sorts the specified list into ascending order, according to the [natural ordering](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html) of its elements.
4. &#x20;[`sort`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#sort-java.util.List-java.util.Comparator-)`(`[`List`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html)`<T> list,` [`Comparator`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)`<? super T> c)`Sorts the specified list according to the order induced by the specified comparator.
5. &#x20;[`swap`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#swap-java.util.List-int-int-)`(`[`List`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html)`<?> list, int i, int j)`Swaps the elements at the specified positions in the specified list.
6. &#x20;[`disjoint`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#disjoint-java.util.Collection-java.util.Collection-)`(`[`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html)`<?> c1,` [`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html)`<?> c2)`Returns `true` if the two specified collections have no elements in common.
7. &#x20;[`fill`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#fill-java.util.List-T-)`(`[`List`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html)`<? super T> list, T obj)`Replaces all of the elements of the specified list with the specified element.
8. &#x20;[`reverse`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#reverse-java.util.List-)`(`[`List`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html)`<?> list)`Reverses the order of the elements in the specified list.

## Comparator and Comparable interface

1. Most common methods from Comparator interface: compare(T o1, T o2), equals(Object object)&#x20;
2. Most common methods from Comparable interface: compareTo(T o).&#x20;
3.  lamda expression. Following expression can order from small to large

    ```java
    (tv1, tv2) -> {
        return tv1.getSize() - tv2.getSize();
    }
    ```

### Examples:

```java
// 1) Comparable interface
class HDTV implements Comparable<HDTV> {
    @Override
    public int compareTo(HDTV tv) {
        if (this.getSize() > tv.getSize()) return 1;
        if (this.getSize() < tv.getSize()) return -1;
        return 0;
    }
}
// 2) Comparator interface
class SizeComparator implements Comparator<HDTV> {
    @Override
    public int compare(HDTV tv1, HDTV tv2) {
        int tv1Size = tv1.getSize(), tv2Size = tv2.getSize();
        if (tv1Size > tv2Size)  return 1;
        if (tv1Size < tv2Size)  return -1;
        return 0;
    }
}
```





