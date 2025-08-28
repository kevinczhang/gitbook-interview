# Ranges

The [`range`](https://docs.python.org/3/library/stdtypes.html#range) type represents an immutable sequence of numbers and is commonly used for looping a specific number of times in [`for`](https://docs.python.org/3/reference/compound_stmts.html#for) loops.

The most common "interactions" or "properties" you'll use with a `range` object are:

1.  Creating a `range` object:

    * `range(stop)`: Generates numbers from 0 up to (but not including) `stop`.
    * `range(start, stop)`: Generates numbers from `start` up to (but not including) `stop`.
    * `range(start, stop, step)`: Generates numbers from `start` up to (but not including) `stop`, incrementing by `step` each time.

    _Example:_

    Python

    ```python
    r1 = range(5)          # 0, 1, 2, 3, 4
    r2 = range(1, 6)       # 1, 2, 3, 4, 5
    r3 = range(0, 10, 2)   # 0, 2, 4, 6, 8
    ```
2. Iterating over a `range` (most common use!):
   * You use `range` directly in `for` loops.
   *   _Example:_

       Python

       ```python
       for i in range(3):
           print(i)
       # Output:
       # 0
       # 1
       # 2
       ```
3. Checking membership (using `in`):
   * You can efficiently check if a number is within the `range`.
   *   _Example:_

       Python

       ```python
       my_range = range(10) # 0 to 9
       print(5 in my_range)  # Output: True
       print(10 in my_range) # Output: False
       ```
4. Accessing elements by index (like a list, but read-only):
   * You can get an element at a specific index, just like with a list, but you can't assign to it.
   *   _Example:_

       Python

       ```python
       my_range = range(10, 20) # 10, 11, ..., 19
       print(my_range[0])  # Output: 10
       print(my_range[5])  # Output: 15
       ```
5. `index(value)` and `count(value)`:
   * Similar to tuples, `range` objects also have these two methods. `index()` finds the first occurrence of a value, and `count()` tells you how many times a value appears (which will be 0 or 1 for a `range` since all numbers are unique by definition of a range).
   *   _Example:_

       Python

       ```python
       my_range = range(0, 10, 2) # 0, 2, 4, 6, 8
       print(my_range.index(4))   # Output: 2 (because 4 is at index 2 in 0,2,4,6,8)
       print(my_range.count(6))   # Output: 1
       print(my_range.count(7))   # Output: 0
       ```

In essence, `range` objects are mostly used to generate sequences of numbers for looping, and they act like immutable sequences with very few direct "methods" for modification, focusing more on their properties for iteration.
