# List Interface

## Implementations

```java
public interface List<E> extends Collection<E>
```

Commonly used implementations: **ArrayList, LinkedList, Vector, Stack.**

* **Vector** is same as ArrayList, except that it contains synchronized methods.
* **Stack** extends Vector and its commonly used methods are: empty(), peek(), pop(), push(), and search().&#x20;

## List methods

1. &#x20;[`add`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html#add-int-E-)`(int index,` [`E`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html) `element)`Inserts the specified element at the specified position in this list (optional operation).
2. &#x20;[`addAll`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html#addAll-int-java.util.Collection-)`(int index,` [`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html)`<? extends` [`E`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html)`> c)`Inserts all of the elements in the specified collection into this list at the specified position (optional operation).
3. &#x20;[`get`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html#get-int-)`(int index)`Returns the element at the specified position in this list.
4. &#x20;[`indexOf`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html#indexOf-java.lang.Object-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) `o)`Returns the index of the first occurrence of the specified element in this list, or -1 if this list does not contain the element.
5. &#x20;[`listIterator`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html#listIterator--)`()`Returns a list iterator over the elements in this list (in proper sequence). &#x20;
6. &#x20;[`listIterator`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html#listIterator-int-)`(int index)`Returns a list iterator over the elements in this list (in proper sequence), starting at the specified position in the list.
7. &#x20;[`remove`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html#remove-int-)`(int index)`Removes the element at the specified position in this list (optional operation).
8. &#x20;[`set`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html#set-int-E-)`(int index,` [`E`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html) `element)`Replaces the element at the specified position in this list with the specified element (optional operation).
9. &#x20;[`sort`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html#sort-java.util.Comparator-)`(`[`Comparator`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)`<? super` [`E`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html)`> c)`Sorts this list according to the order induced by the specified [`Comparator`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html).
10. &#x20;[`subList`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html#subList-int-int-)`(int fromIndex, int toIndex)`Returns a view of the portion of this list between the specified fromIndex, inclusive, and toIndex, exclusive.

## **Differences between Iterator and ListIterator**

### **ListIterator interface has the following Methods:**

* **void add(E e)**: Inserts the specified element into the list.
* **boolean hasNext()**: Returns true if this list iterator has more elements when traversing the list in the forward direction.
* **boolean hasPrevious()**: Returns true if this list iterator has more elements when traversing the list in the reverse direction.
* **E next()**: Returns the next element in the list and advances the cursor position.
* **int nextIndex()**: Returns the index of the element that would be returned by a subsequent call to next().
* **E previous()**: Returns the previous element in the list and moves the cursor position backwards.
* **int previousIndex()**: Returns the index of the element that would be returned by a subsequent call to previous().
* **void remove()**: Removes from the list the last element that was returned by next() or previous().
* **void set(E e)**: Replaces the last element returned by next() or previous() with the specified element.

### Comparison

| ITERATOR                                        | LISTITERATOR                                                |
| ----------------------------------------------- | ----------------------------------------------------------- |
| It supports only Forward Direction Iteration.   | It supports both Forward and Backward Direction iterations. |
| It’s a Uni-Directional Iterator.                | It’s a Bi-Directional Iterator.                             |
| It supports only READ and DELETE operations.    | It supports all CRUD operations.                            |
| We can get Iterator by using iterator() method. | We can ListIterator object using listIterator() method.     |

