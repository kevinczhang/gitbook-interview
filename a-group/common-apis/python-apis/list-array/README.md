---
description: >-
  There are three basic sequence types: lists, tuples, and range objects.
  Additional sequence types tailored for processing of binary data and text
  strings are described in dedicated sections.
---

# Sequence Types

## Common Sequence Operations for all

&#x20;The operations in the following table are supported by most sequence types, both mutable and immutable.&#x20;

<table data-header-hidden><thead><tr><th width="198">Operation</th><th width="563">Result</th></tr></thead><tbody><tr><td>Operation</td><td>Result</td></tr><tr><td><code>x in s</code></td><td><code>True</code> if an item of <em>s</em> is equal to <em>x</em>, else <code>False</code></td></tr><tr><td><code>x not in s</code></td><td><code>False</code> if an item of <em>s</em> is equal to <em>x</em>, else <code>True</code></td></tr><tr><td><code>s + t</code></td><td>the concatenation of <em>s</em> and <em>t</em></td></tr><tr><td><code>s * n</code> or <code>n * s</code></td><td>equivalent to adding <em>s</em> to itself <em>n</em> times</td></tr><tr><td><code>s[i]</code></td><td><em>i</em>th item of <em>s</em>, origin 0</td></tr><tr><td><code>s[i:j]</code></td><td>slice of <em>s</em> from <em>i</em> to <em>j</em></td></tr><tr><td><code>s[i:j:k]</code></td><td>slice of <em>s</em> from <em>i</em> to <em>j</em> with step <em>k</em></td></tr><tr><td><code>len(s)</code></td><td>length of <em>s</em></td></tr><tr><td><code>min(s)</code></td><td>smallest item of <em>s</em></td></tr><tr><td><code>max(s)</code></td><td>largest item of <em>s</em></td></tr><tr><td><code>s.index(x[, i[, j]])</code></td><td>index of the first occurrence of <em>x</em> in <em>s</em> (at or after index <em>i</em> and before index <em>j</em>)</td></tr><tr><td><code>s.count(x)</code></td><td>total number of occurrences of <em>x</em> in <em>s</em></td></tr></tbody></table>

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
