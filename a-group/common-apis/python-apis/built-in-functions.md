# Numbers

There are three distinct numeric types: _integers_, _floating-point numbers_, and _complex numbers_. In addition, Booleans are a subtype of integers.

```python
print(2.1 / 0.2)  # This will print 10.5, which is the result of the division.
# Note: In Python, using // for division will perform floor division.
print(2.1 // 0.2)  # This will print 10.0.

divmod(x, y)  # returns the pair (x // y, x % y)
```

| [`math.floor(x)`](https://docs.python.org/3/library/math.html#math.floor) | the greatest [`Integral`](https://docs.python.org/3/library/numbers.html#numbers.Integral) <= _x_ |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| [`math.ceil(x)`](https://docs.python.org/3/library/math.html#math.ceil)   | the least [`Integral`](https://docs.python.org/3/library/numbers.html#numbers.Integral) >= _x_    |

#### Bitwise Operations on Integer Types

| Operation | Result                                | Notes  |
| --------- | ------------------------------------- | ------ |
| `x \| y`  | bitwise _or_ of _x_ and _y_           | (4)    |
| `x ^ y`   | bitwise _exclusive or_ of _x_ and _y_ | (4)    |
| `x & y`   | bitwise _and_ of _x_ and _y_          | (4)    |
| `x << n`  | _x_ shifted left by _n_ bits          | (1)(2) |
| `x >> n`  | _x_ shifted right by _n_ bits         | (1)(3) |
| `~x`      | the bits of _x_ inverted              |        |

\
