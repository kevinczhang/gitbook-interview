---
description: >-
  Strings are immutable sequences of Unicode code points. String literals are
  written in a variety of ways:
---

# String

* Single quotes: `'allows embedded "double" quotes'`
* Double quotes: `"allows embedded 'single' quotes"`
* Triple quoted: `'''Three single quotes'''`, `"""Three double quotes"""`

Triple quoted strings may span multiple lines - all associated whitespace will be included in the string literal.

## Commonly used methods

Here are some of the most common and useful string methods for competitive programming:

1. `len(s)` (Built-in function, not a method, but crucial!): Returns the length (number of characters) of the string.
   * _Example:_ `len("hello")` is `5`
2. `s.lower()` / `s.upper()`: Returns a new string with all cased characters converted to lowercase/uppercase.
   * _Why useful:_ Case-insensitive comparisons (e.g., checking if two words are the same regardless of case).
   * _Example:_ `"Hello".lower()` is `"hello"`
3. `s.strip()` / `s.lstrip()` / `s.rstrip()`: Returns a new string with leading/trailing whitespace (or specified characters) removed.
   * _Why useful:_ Cleaning up input strings.
   * _Example:_ `" hello world ".strip()` is `"hello world"`
4. `s.split(separator=None)`: Returns a list of substrings by splitting the string at the specified `separator`. If no separator is given, it splits by whitespace.
   * _Why useful:_ Parsing text into words or tokens.
   * _Example:_ `"apple,banana,cherry".split(',')` is `['apple', 'banana', 'cherry']`
5. `s.join(iterable)`: A very powerful method! It concatenates the strings in an `iterable` (like a list of strings), using the string `s` as a separator.
   * _Why useful:_ Building a single string from a list of words. This is often more efficient than repeated string concatenation with `+`.
   * _Example:_ `", ".join(["apple", "banana"])` is `"apple, banana"`
6. `s.find(substring)` / `s.index(substring)`: Returns the lowest index in the string where `substring` is found. `find()` returns `-1` if not found, while `index()` raises a `ValueError` (similar to list's `index`).
   * _Why useful:_ Locating substrings.
   * _Example:_ `"hello world".find("world")` is `6`
7. `s.replace(old, new[, count])`: Returns a new string with all occurrences of `old` substring replaced by `new` substring. `count` limits the number of replacements.
   * _Why useful:_ Modifying specific parts of a string.
   * _Example:_ `"banana".replace('a', 'o')` is `"bonono"`
8. `s.startswith(prefix)` / `s.endswith(suffix)`: Checks if the string starts/ends with a given prefix/suffix. Returns `True` or `False`.
   * _Why useful:_ Pattern matching at string boundaries.
   * _Example:_ `"filename.txt".endswith(".txt")` is `True`
9. `s.isalnum()` / `s.isalpha()` / `s.isdigit()` / `s.isspace()`: These check if all characters in the string are alphanumeric, alphabetic, digits, or whitespace, respectively. Returns `True` or `False`.
   * _Why useful:_ Validating string content (e.g., checking if a password contains only digits).
   * _Example:_ `"12345".isdigit()` is `True`; `"hello".isalpha()` is `True`
