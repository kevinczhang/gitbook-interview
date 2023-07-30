# Linear sort

## **Counting sort**

**Counting sort** assumes that each of the n input elements is an integer in the range 0 to k, for some integer k. When k = O(n), the sort runs in ~~O~~(n) time.

### COUNTING-SORT(A, B, k)

```bash
let C[0 .. k] be a new array
for i = 0 to k
    C[i] = 0
for j = 1 to A.length
    C[A[j]] = C[A[j]] + 1
// C[i] now contains the number of elements equal to i
for i = 1 to k
    C[i] = C[i] + C[i-1]
// C[i] now contains the number of elements less than or equal to i
for j = A.length downto 1
    B[C[A[j]]] = A[j]
    C[A[j]] = C[A[j]] - 1
```

An important property of counting sort is that it is stable: numbers with the same value appear in the output array in the same order as they do in the input array.

running time is $$\Theta(n)$$.

## Radix sort

Radix sort solves the problem of card sorting—counterintuitively—by sorting on the least significant digit first. The process continues until the cards have been sorted on all d digits.

In order for radix sort to work correctly, the digit sorts must be stable.

### RADIX-SORT(A, d)

```bash
for i = 1 to d
    use a stable sort to sort array A on digit i // like counting sort
```

Given n d-digit numbers in which each digit can take on up to k possible values, RADIX-SORT correctly sorts these numbers in $$\Theta(d(n+k))$$ time if the stable sort it uses takes $$\Theta(n+k)$$  time.

## Bucket sort

Bucket sort assumes that the input is drawn from a uniform distribution and has an average-case running time of O(n). Average running time is $$\Theta(n)$$.

### BUCKET-SORT(A)

```bash
let B[0 .. n] be a new array
n = A.length
for i = 0 to n - 1
    make B[i] an empty list
for i = 1 to n
    insert A[i] into list B[nA[i]]
for i = 0 to n - 1
    sort list B[i] with insertion sort
concatenate the lists B[0], B[1], ..., B[n - 1] together in order
```

