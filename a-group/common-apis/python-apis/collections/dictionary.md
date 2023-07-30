---
description: >-
  Dictionary is a collection which is unordered, changeable and indexed. No
  duplicate members.
---

# Mapping Types

## Commonly used methods

| Method                                                                           | Description                                                                                                 |
| -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| [clear()](https://www.w3schools.com/python/ref\_dictionary\_clear.asp)           | Removes all the elements from the dictionary                                                                |
| [copy()](https://www.w3schools.com/python/ref\_dictionary\_copy.asp)             | Returns a copy of the dictionary                                                                            |
| [fromkeys()](https://www.w3schools.com/python/ref\_dictionary\_fromkeys.asp)     | Returns a dictionary with the specified keys and values                                                     |
| [get()](https://www.w3schools.com/python/ref\_dictionary\_get.asp)               | Returns the value of the specified key                                                                      |
| [items()](https://www.w3schools.com/python/ref\_dictionary\_items.asp)           | Returns a list containing a tuple for each key value pair                                                   |
| [keys()](https://www.w3schools.com/python/ref\_dictionary\_keys.asp)             | Returns a list containing the dictionary's keys                                                             |
| [pop()](https://www.w3schools.com/python/ref\_dictionary\_pop.asp)               | Removes the element with the specified key                                                                  |
| [popitem()](https://www.w3schools.com/python/ref\_dictionary\_popitem.asp)       | Removes the last inserted key-value pair                                                                    |
| [setdefault()](https://www.w3schools.com/python/ref\_dictionary\_setdefault.asp) | Returns the value of the specified key. If the key does not exist: insert the key, with the specified value |
| [update()](https://www.w3schools.com/python/ref\_dictionary\_update.asp)         | Updates the dictionary with the specified key-value pairs                                                   |
| [values()](https://www.w3schools.com/python/ref\_dictionary\_values.asp)         | Returns a list of all the values in the dictionary                                                          |

```python
>>> a = dict(one=1, two=2, three=3)
>>> b = {'one': 1, 'two': 2, 'three': 3}
>>> c = dict(zip(['one', 'two', 'three'], [1, 2, 3]))
>>> d = dict([('two', 2), ('one', 1), ('three', 3)])
>>> e = dict({'three': 3, 'one': 1, 'two': 2})
>>> a == b == c == d == e
True
```

