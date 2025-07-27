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
