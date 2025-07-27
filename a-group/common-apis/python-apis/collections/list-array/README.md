---
description: >-
  There are three basic sequence types: lists, tuples, and range objects.
  Additional sequence types tailored for processing of binary data and text
  strings are described in dedicated sections.
---

# Sequence Types

## Common Sequence Operations for all

&#x20;The operations in the following table are supported by most sequence types, both mutable and immutable. The [`collections.abc.Sequence`](https://docs.python.org/3/library/collections.abc.html#collections.abc.Sequence) ABC is provided to make it easier to correctly implement these operations on custom sequence types.

| Operation              | Result                                                                                   |
| ---------------------- | ---------------------------------------------------------------------------------------- |
| `x in s`               | `True` if an item of _s_ is equal to _x_, else `False`                                   |
| `x not in s`           | `False` if an item of _s_ is equal to _x_, else `True`                                   |
| `s + t`                | the concatenation of _s_ and _t_                                                         |
| `s * n` or `n * s`     | equivalent to adding _s_ to itself _n_ times                                             |
| `s[i]`                 | _&#x69;_&#x74;h item of _s_, origin 0                                                    |
| `s[i:j]`               | slice of _s_ from _i_ to _j_                                                             |
| `s[i:j:k]`             | slice of _s_ from _i_ to _j_ with step _k_                                               |
| `len(s)`               | length of _s_                                                                            |
| `min(s)`               | smallest item of _s_                                                                     |
| `max(s)`               | largest item of _s_                                                                      |
| `s.index(x[, i[, j]])` | index of the first occurrence of _x_ in _s_ (at or after index _i_ and before index _j_) |
| `s.count(x)`           | total number of occurrences of _x_ in _s_                                                |

## Mutable Sequence Types Methods

| Operation                 | Result                                                                                     | Notes |
| ------------------------- | ------------------------------------------------------------------------------------------ | ----- |
| `s[i] = x`                | item _i_ of _s_ is replaced by _x_                                                         |       |
| `s[i:j] = t`              | slice of _s_ from _i_ to _j_ is replaced by the contents of the iterable _t_               |       |
| `del s[i:j]`              | same as `s[i:j] = []`                                                                      |       |
| `s[i:j:k] = t`            | the elements of `s[i:j:k]` are replaced by those of _t_                                    | (1)   |
| `del s[i:j:k]`            | removes the elements of `s[i:j:k]` from the list                                           |       |
| `s.append(x)`             | appends _x_ to the end of the sequence (same as `s[len(s):len(s)] = [x]`)                  |       |
| `s.clear()`               | removes all items from _s_ (same as `dels[:]`)                                             | (5)   |
| `s.copy()`                | creates a shallow copy of _s_ (same as `s[:]`)                                             | (5)   |
| `s.extend(t)` or `s += t` | extends _s_ with the contents of _t_ (for the most part the same as`s[len(s):len(s)] = t`) |       |
| `s *= n`                  | updates _s_ with its contents repeated _&#x6E;_&#x74;imes                                  | (6)   |
| `s.insert(i, x)`          | inserts _x_ into _s_ at the index given by _i_(same as `s[i:i] = [x]`)                     |       |
| `s.pop([i])`              | retrieves the item at _i_ and also removes it from _s_                                     | (2)   |
| `s.remove(x)`             | remove the first item from _s_ where `s[i]`is equal to _x_                                 | (3)   |
| `s.reverse()`             | reverses the items of _s_ in place                                                         | (4)   |

## Lists commonly used methods

&#x20;The `sort()` method sorts the list ascending by default.  _list_.sort(reverse=True|False, key=myFunc)

### Parameter Values

| Parameter | Description                                                                    |
| --------- | ------------------------------------------------------------------------------ |
| reverse   | Optional. reverse=True will sort the list descending. Default is reverse=False |
| key       | Optional. A function to specify the sorting criteria(s)                        |

```python
# A function that returns the length of the value:
def myFunc(e):
  return len(e)

cars = ['Ford', 'Mitsubishi', 'BMW', 'VW']

cars.sort(reverse=True, key=myFunc)
```

## Tuples

&#x20;Tuples are immutable sequences, typically used to store collections of heterogeneous data. such as the 2-tuples produced by the [`enumerate()`](https://docs.python.org/3/library/functions.html#enumerate) built-in)

## Ranges

&#x20;The [`range`](https://docs.python.org/3/library/stdtypes.html#range) type represents an immutable sequence of numbers and is commonly used for looping a specific number of times in [`for`](https://docs.python.org/3/reference/compound_stmts.html#for) loops.

```python
>>> list(range(10))
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> list(range(1, 11))
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
>>> list(range(0, 30, 5))
[0, 5, 10, 15, 20, 25]
>>> list(range(0, 10, 3))
[0, 3, 6, 9]
>>> list(range(0, -10, -1))
[0, -1, -2, -3, -4, -5, -6, -7, -8, -9]
>>> list(range(0))
[]
>>> list(range(1, 0))
[]

```
