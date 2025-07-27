# Counter

A counter tool is provided to support convenient and rapid tallies. For example:

```python
# Tally occurrences of words in a list
cnt = Counter()
for word in ['red', 'blue', 'red', 'green', 'blue', 'blue']:
    cnt[word] += 1

cnt
Counter({'blue': 3, 'red': 2, 'green': 1})

# Find the ten most common words in Hamlet
import re
words = re.findall(r'\w+', open('hamlet.txt').read().lower())
Counter(words).most_common(10)
[('the', 1143), ('and', 966), ('to', 762), ('of', 669), ('i', 631),
 ('you', 554),  ('a', 546), ('my', 514), ('hamlet', 471), ('in', 451)]
 
 
from collections import Counter

# From a list
numbers = [1, 2, 2, 3, 1, 4, 2]
num_counts = Counter(numbers)
print(num_counts) # Output: Counter({2: 3, 1: 2, 3: 1, 4: 1})

# From a string (like our previous example!)
text = "hello world"
char_counts = Counter(text)
print(char_counts) 
# Output: Counter({'l': 3, 'o': 2, 'h': 1, 'e': 1, ' ': 1, 'w': 1, 'r': 1, 'd': 1})
```
