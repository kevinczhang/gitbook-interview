---
description: >-
  Mappings are mutable objects. There is currently only one standard mapping
  type, the dictionary.
---

# Mapping Types

A [mapping](https://docs.python.org/3/glossary.html#term-mapping) object maps [hashable](https://docs.python.org/3/glossary.html#term-hashable) values to arbitrary objects.&#x20;

```python
>>> a = dict(one=1, two=2, three=3)
>>> b = {'one': 1, 'two': 2, 'three': 3}
>>> c = dict(zip(['one', 'two', 'three'], [1, 2, 3]))
>>> d = dict([('two', 2), ('one', 1), ('three', 3)])
>>> e = dict({'three': 3, 'one': 1, 'two': 2})
>>> a == b == c == d == e
True
```

## Commonly used methods

Here are the most commonly used dictionary methods, especially for LeetCode problems:

1. `dict.get(key, default=None)`:
   * Returns the `value` for the specified `key`.
   * Crucially, if the `key` is not found, it returns `default` (which is `None` if not specified) instead of raising a `KeyError`. This makes it safer than direct `dict[key]` access when a key might be missing.
   * _Why useful:_ Safely retrieving values, especially when counting frequencies or handling optional keys.
   *   _Example:_

       Python

       ```python
       grades = {"Alice": 90, "Bob": 85}
       print(grades.get("Alice"))     # Output: 90
       print(grades.get("Charlie"))   # Output: Output: None
       print(grades.get("Charlie", 0))# Output: 0 (default value if not found)
       ```
2. `dict.keys()`:
   * Returns a view object that displays a list of all the keys in the dictionary.
   * _Why useful:_ Iterating over keys.
   * _Example:_ `grades.keys()` might show `dict_keys(['Alice', 'Bob'])`
3. `dict.values()`:
   * Returns a view object that displays a list of all the values in the dictionary.
   * _Why useful:_ Iterating over values.
   * _Example:_ `grades.values()` might show `dict_values([90, 85])`
4. `dict.items()`:
   * Returns a view object that displays a list of a dictionary's key-value tuple pairs. This is often used with tuple unpacking in `for` loops.
   * _Why useful:_ Iterating over both keys and values simultaneously.
   *   _Example:_

       Python

       ```python
       grades = {"Alice": 90, "Bob": 85}
       for name, score in grades.items():
           print(f"{name}: {score}")
       # Output:
       # Alice: 90
       # Bob: 85
       ```
5. `dict.update(other_dict)`:
   * Updates the dictionary with elements from another dictionary or from an iterable of key-value pairs. If a key already exists, its value is updated; otherwise, new key-value pairs are added.
   * _Why useful:_ Merging dictionaries.
   *   _Example:_

       Python

       ```python
       d1 = {"a": 1, "b": 2}
       d2 = {"b": 3, "c": 4}
       d1.update(d2) # d1 is now {'a': 1, 'b': 3, 'c': 4}
       ```
6. `dict.pop(key[, default])`:
   * Removes the specified `key` and returns its corresponding `value`. If `key` is not found, `default` is returned if provided, otherwise a `KeyError` is raised.
   * _Why useful:_ Removing an item while also retrieving its value.
   * _Example:_ `grades.pop("Alice")` returns `90` and removes "Alice" from `grades`.
7. `dict.clear()`:
   * Removes all items from the dictionary.
   * _Why useful:_ Resetting a dictionary.

For LeetCode, `get()`, `keys()`, `values()`, and `items()` are used very frequently for iteration and safe access. The `update()` method is also handy for combining information.
