---
description: >-
  Defines size, enumerators, and synchronization methods for all nongeneric
  collections.
---

# ICollection Interface

## Overview of ICollection

The [ICollection](https://docs.microsoft.com/en-us/dotnet/api/system.collections.icollection?view=netcore-2.2) interface is the base interface for classes in the [System.Collections](https://docs.microsoft.com/en-us/dotnet/api/system.collections?view=netcore-2.2) namespace. Its generic equivalent is the [System.Collections.Generic.ICollection\<T>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.icollection-1?view=netcore-2.2) interface. The [ICollection](https://docs.microsoft.com/en-us/dotnet/api/system.collections.icollection?view=netcore-2.2) interface extends [IEnumerable](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerable?view=netcore-2.2).

&#x20;[IDictionary](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary?view=netcore-2.2) and [IList](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist?view=netcore-2.2) are more specialized interfaces that extend [ICollection](https://docs.microsoft.com/en-us/dotnet/api/system.collections.icollection?view=netcore-2.2). &#x20;

Some collections that limit access to their elements, such as the [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2) class and the [Stack](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack?view=netcore-2.2) class, directly implement the [ICollection](https://docs.microsoft.com/en-us/dotnet/api/system.collections.icollection?view=netcore-2.2) interface.

### Properties  <a href="#properties" id="properties"></a>

| [Count](https://docs.microsoft.com/en-us/dotnet/api/system.collections.icollection.count?view=netcore-2.2#System\_Collections\_ICollection\_Count) | Gets the number of elements contained in the [ICollection](https://docs.microsoft.com/en-us/dotnet/api/system.collections.icollection?view=netcore-2.2). |
| -------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |

## Queue Class

&#x20;This class implements a queue as a circular array. Objects stored in a [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2) are inserted at one end and removed from the other. Three main operations can be performed on a [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2) and its elements:

* [Enqueue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue.enqueue?view=netcore-2.2) adds an element to the end of the [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2).
* [Dequeue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue.dequeue?view=netcore-2.2) removes the oldest element from the start of the [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2).
* [Peek](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue.peek?view=netcore-2.2) returns the oldest element that is at the start of the [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2) but does not remove it from the [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2).

### Methods  <a href="#methods" id="methods"></a>

| [Clear()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue.clear?view=netcore-2.2#System\_Collections\_Queue\_Clear)                                                         | Removes all objects from the [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2).                                                                                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Clone()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue.clone?view=netcore-2.2#System\_Collections\_Queue\_Clone)                                                         | Creates a shallow copy of the [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2).                                                                                                                                                |
| [Contains(Object)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue.contains?view=netcore-2.2#System\_Collections\_Queue\_Contains\_System\_Object\_)                        | Determines whether an element is in the [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2).                                                                                                                                      |
| [CopyTo(Array, Int32)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue.copyto?view=netcore-2.2#System\_Collections\_Queue\_CopyTo\_System\_Array\_System\_Int32\_)          | Copies the [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2) elements to an existing one-dimensional [Array](https://docs.microsoft.com/en-us/dotnet/api/system.array?view=netcore-2.2), starting at the specified array index. |
| [Dequeue()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue.dequeue?view=netcore-2.2#System\_Collections\_Queue\_Dequeue)                                                   | Removes and returns the object at the beginning of the [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2).                                                                                                                       |
| [Enqueue(Object)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue.enqueue?view=netcore-2.2#System\_Collections\_Queue\_Enqueue\_System\_Object\_)                           | Adds an object to the end of the [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2).                                                                                                                                             |
| [GetEnumerator()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue.getenumerator?view=netcore-2.2#System\_Collections\_Queue\_GetEnumerator)                                 | Returns an enumerator that iterates through the [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2).                                                                                                                              |
| [Peek()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue.peek?view=netcore-2.2#System\_Collections\_Queue\_Peek)                                                            | Returns the object at the beginning of the [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2) without removing it.                                                                                                               |
| [Synchronized(Queue)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue.synchronized?view=netcore-2.2#System\_Collections\_Queue\_Synchronized\_System\_Collections\_Queue\_) | Returns a new [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2) that wraps the original queue, and is thread safe.                                                                                                              |
| [ToArray()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue.toarray?view=netcore-2.2#System\_Collections\_Queue\_ToArray)                                                   | Copies the [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2) elements to a new array.                                                                                                                                           |
| [TrimToSize()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue.trimtosize?view=netcore-2.2#System\_Collections\_Queue\_TrimToSize)                                          | Sets the capacity to the actual number of elements in the [Queue](https://docs.microsoft.com/en-us/dotnet/api/system.collections.queue?view=netcore-2.2).                                                                                                                    |

## Stack Class

### Methods  <a href="#methods" id="methods"></a>

| [Clear()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack.clear?view=netcore-2.2#System\_Collections\_Stack\_Clear)                                                         | Removes all objects from the [Stack](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack?view=netcore-2.2).                                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Clone()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack.clone?view=netcore-2.2#System\_Collections\_Stack\_Clone)                                                         | Creates a shallow copy of the [Stack](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack?view=netcore-2.2).                                                                                                                                       |
| [Contains(Object)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack.contains?view=netcore-2.2#System\_Collections\_Stack\_Contains\_System\_Object\_)                        | Determines whether an element is in the [Stack](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack?view=netcore-2.2).                                                                                                                             |
| [CopyTo(Array, Int32)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack.copyto?view=netcore-2.2#System\_Collections\_Stack\_CopyTo\_System\_Array\_System\_Int32\_)          | Copies the [Stack](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack?view=netcore-2.2) to an existing one-dimensional [Array](https://docs.microsoft.com/en-us/dotnet/api/system.array?view=netcore-2.2), starting at the specified array index. |
| [GetEnumerator()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack.getenumerator?view=netcore-2.2#System\_Collections\_Stack\_GetEnumerator)                                 | Returns an [IEnumerator](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerator?view=netcore-2.2) for the [Stack](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack?view=netcore-2.2).                                       |
| [Peek()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack.peek?view=netcore-2.2#System\_Collections\_Stack\_Peek)                                                            | Returns the object at the top of the [Stack](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack?view=netcore-2.2) without removing it.                                                                                                            |
| [Pop()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack.pop?view=netcore-2.2#System\_Collections\_Stack\_Pop)                                                               | Removes and returns the object at the top of the [Stack](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack?view=netcore-2.2).                                                                                                                    |
| [Push(Object)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack.push?view=netcore-2.2#System\_Collections\_Stack\_Push\_System\_Object\_)                                    | Inserts an object at the top of the [Stack](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack?view=netcore-2.2).                                                                                                                                 |
| [Synchronized(Stack)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack.synchronized?view=netcore-2.2#System\_Collections\_Stack\_Synchronized\_System\_Collections\_Stack\_) | Returns a synchronized (thread safe) wrapper for the [Stack](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack?view=netcore-2.2).                                                                                                                |
| [ToArray()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack.toarray?view=netcore-2.2#System\_Collections\_Stack\_ToArray)                                                   | Copies the [Stack](https://docs.microsoft.com/en-us/dotnet/api/system.collections.stack?view=netcore-2.2) to a new array.                                                                                                                                           |