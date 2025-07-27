---
description: >-
  A set object is an unordered collection of distinct hashable objects. Set is a
  collection which is unordered and unindexed. No duplicate members.
---

# Set Types

## Commonly used methods

The core idea of a set is that it's an unordered collection of unique, hashable elements. This uniqueness and fast lookup are what make them special.

Here are the most common and useful methods for Python sets:

1. `set.add(element)`: Adds an `element` to the set. If the element is already in the set, nothing happens (because sets only store unique items).
   * _Why useful:_ Building up a set of unique items, marking elements as "seen."
   *   _Example:_

       Python

       ```python
       my_set = {1, 2}
       my_set.add(3)  # my_set is now {1, 2, 3}
       my_set.add(2)  # my_set remains {1, 2, 3}
       ```
2. `set.remove(element)`: Removes the specified `element` from the set.
   * _Why useful:_ When you need to take an item out of a unique collection.
   * _Important Note:_ If the `element` is not found in the set, it raises a `KeyError`.
   *   _Example:_

       Python

       ```python
       my_set = {1, 2, 3}
       my_set.remove(2) # my_set is now {1, 3}
       # my_set.remove(5) # This would raise a KeyError
       ```
3. `set.discard(element)`: Also removes the specified `element` from the set.
   * _Why useful:_ It's similar to `remove()`, but `discard()` does not raise an error if the element is not found. This makes it safer if you're not sure if an element is present.
   *   _Example:_

       Python

       ```python
       my_set = {1, 2, 3}
       my_set.discard(2) # my_set is now {1, 3}
       my_set.discard(5) # my_set remains {1, 3}, no error
       ```
4. `set.pop()`: Removes and returns an arbitrary (random) element from the set.
   * _Why useful:_ When you just need _an_ element and don't care which one.
   * _Important Note:_ Raises a `KeyError` if the set is empty.
   *   _Example:_

       Python

       ```python
       my_set = {1, 2, 3}
       element = my_set.pop() # element will be 1, 2, or 3, my_set will have 2 elements left
       ```
5. `set.clear()`: Removes all elements from the set, making it empty.
   * _Why useful:_ Resetting a set.
   *   _Example:_

       Python

       ```python
       my_set = {1, 2, 3}
       my_set.clear() # my_set is now set()
       ```
6. `len(set)` (Built-in function): Returns the number of unique elements in the set.
7.  Set Operations (for combining/comparing sets): These return _new_ sets.

    * `set.union(other_set)` or `set | other_set`: Returns a new set containing all unique elements from both sets.
    * `set.intersection(other_set)` or `set & other_set`: Returns a new set containing only the elements common to both sets.
    * `set.difference(other_set)` or `set - other_set`: Returns a new set containing elements in the first set but not in the `other_set`.
    * `set.symmetric_difference(other_set)` or `set ^ other_set`: Returns a new set containing elements that are in _either_ set, but not in both.

    _Example:_

    Python

    ```python
    set_a = {1, 2, 3}
    set_b = {3, 4, 5}
    print(set_a.union(set_b))       # {1, 2, 3, 4, 5}
    print(set_a.intersection(set_b)) # {3}
    print(set_a.difference(set_b))   # {1, 2}
    ```

For LeetCode, `add()`, `remove()`/`discard()`, `pop()`, and the `in` operator for fast membership testing are your most frequent companions when dealing with sets. The set operations are also incredibly useful for problems involving unique elements across different collections.
