---
description: >-
  In Python, bit manipulation involves using bitwise operators to work with the
  individual bits of an integer.
---

# bit manipulation

This is useful for tasks like optimizing algorithms, low-level programming, and solving certain types of coding challenges. Python's built-in bitwise operators make this process straightforward.

#### Understanding Bitwise Operators

Python provides six bitwise operators for performing bit-level operations:

* AND (`&`): This operator performs a bit-by-bit AND operation. The resulting bit is 1 only if both corresponding bits are 1. For example, `5 & 3` is `1`. In binary, `5` is `0101` and `3` is `0011`. The bitwise AND is `0001`, which is `1`.
* OR (`|`): This operator performs a bit-by-bit OR operation. The resulting bit is 1 if at least one of the corresponding bits is 1. For example, `5 | 3` is `7`. In binary, `0101` OR `0011` is `0111`, which is `7`.
* XOR (`^`): This operator performs a bit-by-bit XOR (exclusive OR) operation. The resulting bit is 1 if the corresponding bits are different. For example, `5 ^ 3` is `6`. In binary, `0101` XOR `0011` is `0110`, which is `6`.
* NOT (`~`): This operator performs a bit-by-bit NOT operation, inverting all the bits. It's important to note that Python represents integers using a two's complement system, which can sometimes lead to unexpected results if you're not familiar with it. For example, `~5` is `-6`. This is because `5` is `...00000101`, and `~5` is `...11111010`, which in two's complement is `-6`.
* Left Shift (`<<`): This operator shifts the bits of a number to the left by a specified number of positions, filling the new positions with zeros. This is equivalent to multiplying the number by $$2n$$, where $$n$$ is the number of positions shifted. For example, `5 << 2` is `20`. In binary, `0101` shifted left by two is `010100`, which is `20`.
* Right Shift (`>>`): This operator shifts the bits of a number to the right by a specified number of positions. This is equivalent to integer division by $$2n$$, where $$n$$ is the number of positions shifted. For example, `5 >> 2` is `1`. In binary, `0101` shifted right by two is `0001`, which is `1`.

***

#### Common Bit Manipulation Techniques

You can use these operators to perform various bit manipulation tasks.

**Checking if a bit is set**

To check if the i-th bit of a number n is set (i.e., is 1), you can use the bitwise AND operator with a number that has only the i-th bit set. A common way to create this number is by left-shifting 1 by i positions (1 << i). The expression (n >> i) & 1 is also a valid alternative.

For example, to check if the 3rd bit of n=10 is set:

Python

```
n = 10  # Binary is 1010
i = 3
if (n & (1 << i)):
    print(f"The {i}th bit is set.")
else:
    print(f"The {i}th bit is not set.")
```

***

**Setting a bit**

To set the i-th bit of a number n (change it to 1), you can use the bitwise OR operator. The expression n | (1 << i) will set the bit without affecting the other bits.

For example, to set the 2nd bit of n=8:

Python

```
n = 8  # Binary is 1000
i = 2
result = n | (1 << i)
print(result) # Output: 12 (Binary is 1100)
```

***

**Clearing a bit**

To clear the i-th bit of a number n (change it to 0), you can use the bitwise AND operator with the complement of a number that has only the i-th bit set. The expression n & (\~(1 << i)) will clear the bit.

For example, to clear the 3rd bit of n=10:

Python

```
n = 10  # Binary is 1010
i = 3
result = n & (~(1 << i))
print(result) # Output: 2 (Binary is 0010)
```

***

**Toggling a bit**

To toggle the i-th bit of a number n (flip it from 0 to 1 or 1 to 0), you can use the bitwise XOR operator. The expression n ^ (1 << i) will toggle the bit.

For example, to toggle the 2nd bit of n=10:

Python

```
n = 10  # Binary is 1010
i = 2
result = n ^ (1 << i)
print(result) # Output: 14 (Binary is 1110)
```
