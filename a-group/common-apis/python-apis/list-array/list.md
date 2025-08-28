# List

* List Comprehensions: A concise way to create lists. Imagine you want to create a list of squares from 1 to 10. Instead of a multi-line `for` loop, you can do it in one line!

```python
numbers = [1, 2, 3, 4, 5, 6]
doubled_evens = [num * 2 for num in numbers if num % 2 == 0]
print(doubled_evens) # Output: [4, 8, 12]
```

* `enumerate`: When you need both the item and its index in a loop. It's like getting two birds with one stone!

```python
students = ["Alice", "Bob", "Charlie", "Diana"]
[print(f"Student {index + 1}: {student}") for index, student in enumerate(students)]
```

* `zip`: For iterating over multiple lists simultaneously. This is great when you have related data spread across different lists.

```python
products = ["Laptop", "Mouse", "Keyboard", "Monitor"]
prices = [1200, 25, 75, 300]
[print(f"{product}: ${price}") for product, price in zip(products, prices)]
```

* Efficient Swapping using Tuple Unpacking: A neat trick to swap two variable values without needing a temporary variable. It's like magic!

```python
a = 5
b = 10
a, b = b, a # This is the magic!
print(f"a: {a}, b: {b}") # Output: a: 10, b: 5
```

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

Here are some of the most frequently used and important list methods, especially in the context of solving algorithm problems:

1. `append(item)`: Adds an `item` to the _end_ of the list.
   * _Why it's useful:_ Building a list incrementally.
   * _Example:_ `my_list = [1, 2]; my_list.append(3)` results in `[1, 2, 3]`
2. `extend(iterable)`: Appends all the items from an `iterable` (like another list) to the end of the current list. It's like adding a whole train car to the end of your train.
   * _Why it's useful:_ Concatenating lists efficiently.
   * _Example:_ `my_list = [1, 2]; my_list.extend([3, 4])` results in `[1, 2, 3, 4]`
3. `insert(index, item)`: Inserts an `item` at a specified `index`.
   * _Why it's useful:_ Adding an element precisely where you need it in the middle of a list. (Be aware this can be slow for large lists as elements need to shift).
   * _Example:_ `my_list = [1, 3]; my_list.insert(1, 2)` results in `[1, 2, 3]`
4. `pop([index])`: Removes and returns the item at the given `index`. If no index is specified, it removes and returns the _last_ item.
   * _Why it's useful:_ Implementing stacks (LIFO) or queues (FIFO from one end) or simply removing an element while getting its value.
   * _Example:_ `my_list = [1, 2, 3]; last_item = my_list.pop()` results in `my_list` being `[1, 2]` and `last_item` being `3`. `my_list.pop(0)` would remove `1`.
5. `remove(item)`: Removes the _first occurrence_ of the specified `item` from the list.
   * _Why it's useful:_ Deleting a specific value. (Raises `ValueError` if `item` is not found).
   * _Example:_ `my_list = [1, 2, 3, 2]; my_list.remove(2)` results in `[1, 3, 2]`
6. `index(item, [start[, end]])`: Returns the zero-based index of the _first occurrence_ of `item`. (We just discussed this one!)
   * _Why it's useful:_ Finding the position of an element. (Raises `ValueError` if `item` is not found).
   * _Example:_ `my_list = [10, 20, 30]; print(my_list.index(20))` outputs `1`
7. `count(item)`: Returns the number of times `item` appears in the list.
   * _Why it's useful:_ Tallying occurrences.
   * _Example:_ `my_list = [1, 2, 2, 3]; print(my_list.count(2))` outputs `2`
8. `sort(key=None, reverse=False)`: Sorts the items of the list _in place_ (modifies the original list).
   * _Why it's useful:_ Ordering data.
   * _Example:_ `my_list = [3, 1, 2]; my_list.sort()` results in `[1, 2, 3]`
9. `reverse()`: Reverses the order of elements in the list _in place_.
   * _Why it's useful:_ When you need to process elements from end to start.
   * _Example:_ `my_list = [1, 2, 3]; my_list.reverse()` results in `[3, 2, 1]`
