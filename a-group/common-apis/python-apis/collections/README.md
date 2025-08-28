---
description: >-
  This module implements specialized container datatypes providing alternatives
  to Python’s general purpose built-in containers, dict, list, set, and tuple.
---

# Collections

The `collections` module in Python provides specialized container data types that offer alternatives to the general-purpose built-in containers like `dict`, `list`, `tuple`, and `set`. These specialized classes are optimized for specific use cases, making your code more efficient and readable.

Here are some of the most common and useful classes from the `collections` module:

#### 1. `deque`

A `deque` (short for double-ended queue) is a list-like container with fast appends and pops from either end. Unlike a regular `list`, which is slow for operations at the beginning, a `deque` provides constant-time O(1) performance for `appendleft()` and `popleft()`. This makes it ideal for implementing queues and stacks and for "sliding window" problems in algorithms.

#### 2. `Counter`

A `Counter` is a `dict` subclass designed for counting hashable objects.<sup>1</sup> It's a fantastic tool for counting the occurrences of elements in a sequence, such as characters in a string or words in a list. You can create a `Counter` by passing an iterable to its constructor, and it automatically tallies the items for you. It also has useful methods like `most_common()` to find the most frequent elements.

#### 3. `defaultdict`

A `defaultdict` is a `dict` subclass that overrides a single method to provide a default value for a missing key. This prevents `KeyError` exceptions when you try to access a key that doesn't exist. You initialize a `defaultdict` by providing a factory function (e.g., `int` for a default of `0`, or `list` for a default of an empty list). It's very useful for grouping items or accumulating values in a dictionary.

#### 4. `namedtuple`

The `namedtuple()` is a factory function for creating tuple subclasses with named fields. It allows you to access elements of the tuple by name instead of by index, which makes your code more readable and self-documenting, especially when dealing with data records. It's an immutable object, retaining all the benefits of a regular tuple, such as being a valid dictionary key.

#### 5. `ChainMap`

A `ChainMap` is a class that groups multiple dictionaries or other mappings into a single view.<sup>2</sup> When you perform a lookup, it searches the dictionaries in the order they were provided and returns the first value it finds. This is particularly useful for handling multiple scopes, such as local, global, and default settings, without having to manually merge dictionaries.
