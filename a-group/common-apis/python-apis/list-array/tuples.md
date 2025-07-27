---
description: Tuples are immutable sequences
---

# Tuples

Tuples are immutable sequences, typically used to store collections of heterogeneous data (such as the 2-tuples produced by the [`enumerate()`](https://docs.python.org/3/library/functions.html#enumerate) built-in).

Tuples are also used for cases where an immutable sequence of homogeneous data is needed (such as allowing storage in a [`set`](https://docs.python.org/3/library/stdtypes.html#set) or [`dict`](https://docs.python.org/3/library/stdtypes.html#dict) instance).

The most important thing to remember about tuples is that they are immutable. This means once a tuple is created, you cannot change its elements, add new ones, or remove existing ones. This immutability is why they have fewer methods compared to lists.

Because they are immutable, tuples primarily have only two methods that you'll commonly use:

1. `tuple.count(value)`: Returns the number of times a specified `value` occurs in the tuple.
   * _Why it's useful:_ Counting occurrences of elements.
   *   _Example:_

       Python

       ```python
       my_tuple = (1, 2, 3, 2, 4, 2)
       print(my_tuple.count(2)) # Output: 3
       print(my_tuple.count(5)) # Output: 0
       ```
2. `tuple.index(value, [start[, end]])`: Returns the index of the _first occurrence_ of the specified `value` in the tuple. Just like with lists and strings, you can optionally specify `start` and `end` indices to narrow down the search range.
   * _Why it's useful:_ Finding the position of a specific element.
   * _Important Note:_ If the `value` is not found, it raises a `ValueError`.
   *   _Example:_

       Python

       ```python
       my_tuple = ('a', 'b', 'c', 'a', 'd')
       print(my_tuple.index('a'))    # Output: 0
       print(my_tuple.index('a', 1)) # Output: 3 (starts search from index 1)
       # print(my_tuple.index('z'))  # This would raise a ValueError
       ```

Why are tuples important for LeetCode if they have so few methods?

* Immutability: This makes them suitable as keys in dictionaries (which lists cannot be) and elements in sets, where unique, hashable items are required.
* Tuple Unpacking: As we discussed earlier, this is super Pythonic and common!
* Returning Multiple Values: Functions in Python often return multiple values as a tuple implicitly.
