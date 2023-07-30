---
description: From cracking the interview 18.2
---

# Generate random array

## Description

Write a method to randomly generate a set of m integers from an array of size n. Each element must have equal probability of being chosen.

## Solution



Recursive solution:

```java
// Random number between lower and higher, inclusive
int[] pickMRecursively(int[] original, int m, int i){
    if (i + 1 == m) {

}
```

Iterative Solution

```java
void shuffleArrayIteratively(int[] cards){
    for(int i = 0; i < cards.length; i++){
        int k = rand(0, i);
        int temp = cards[k];
        cards[k] = cards[i];
        cards[i] = temp;
    }
}
```
