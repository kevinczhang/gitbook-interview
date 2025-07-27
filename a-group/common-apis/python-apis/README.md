---
description: In this section, all commonly used Python APIs are listed
---

# Python

## Built-in types heritage

![](<../../../.gitbook/assets/image (35).png>)

Python, a dynamically typed language, automatically infers the data type of a variable based on the value assigned to it. Despite this dynamic typing, Python has a robust system of built-in data types that categorize different kinds of values. Here are the main categories of built-in Python data types:

* **Text Type:**
  * `str`: Used for sequences of characters (text).
* **Numeric Types:**
  * `int`: Represents whole numbers (integers).
  * `float`: Represents numbers with a decimal point (floating-point numbers).
  * `complex`: Represents complex numbers with a real and imaginary part.
* **Sequence Types:**
  * `list`: An ordered, mutable collection of items, allowing duplicates.
  * `tuple`: An ordered, immutable collection of items, allowing duplicates.
  * `range`: Represents an immutable sequence of numbers, often used in loops.
* **Mapping Type:**
  * `dict`: An unordered, mutable collection of key-value pairs.
* **Set Types:**
  * `set`: An unordered, mutable collection of unique items.
  * `frozenset`: An unordered, immutable collection of unique items.
* **Boolean Type:**
  * `bool`: Represents truth values, either `True` or `False`.
* **Binary Types:**
  * `bytes`: An immutable sequence of bytes.
  * `bytearray`: A mutable sequence of bytes.
  * `memoryview`: A view into another object's memory.
* **None Type:**
  * `NoneType`: Represents the absence of a value. The single value of this type is `None`.

You can determine the type of any object or variable in Python using the `type()` function. For example:

## Inheritance

```python
class Person:

    def __init__(self, first, last):
        self.firstname = first
        self.lastname = last

    def Name(self):
        return self.firstname + " " + self.lastname

class Employee(Person):

    def __init__(self, first, last, staffnum):
        Person.__init__(self,first, last)
        self.staffnumber = staffnum

    def GetEmployee(self):
        return self.Name() + ", " +  self.staffnumber

x = Person("Marge", "Simpson")
y = Employee("Homer", "Simpson", "1007")

print(x.Name())
print(y.GetEmployee())
```

