# Sort

## Quick Sort

It’s generally an “in-place” algorithm, with the average time complexity of O(n log n).

Outline of the `partition` method goes something like this:

1. Pick a pivot point.
2. Move all elements that are less than the pivot point to the left side of the partition.
3. Move all elements that are greater than the pivot point to the right side of the partition.
4. Return the index of the pivot point.

```java
public static int partition(int low, int high) {
  int pivot = a[low];
  int i = low - 1;
  int j = high + 1;
  while (i < j) {
    for (i++; a[i] < pivot; i++);
    for (j--; a[j] > pivot; j--);
    if (i < j)
       swap(i, j);
   }
   return j;
}


public static void swap(int i, int j)
{
 int temp = a[i];
 a[i] = a[j];
 a[j] = temp;
}
```

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

#### quickSort()

```java
public void quickSort(int arr[], int begin, int end) {
    if (begin < end) {
        int partitionIndex = partition(arr, begin, end);

        quickSort(arr, begin, partitionIndex-1);
        quickSort(arr, partitionIndex+1, end);
    }
}
```

#### partition()

```java
private int partition(int arr[], int begin, int end) {
    int pivot = arr[end];
    int i = (begin-1);

    for (int j = begin; j < end; j++) {
        if (arr[j] <= pivot) {
            i++;
            int swapTemp = arr[i];
            arr[i] = arr[j];
            arr[j] = swapTemp;
        }
    }

    int swapTemp = arr[i+1];
    arr[i+1] = arr[end];
    arr[end] = swapTemp;

    return i+1;
}
```

### **3-Way QuickSort**

In 3 Way QuickSort, an array arr\[l..r] is divided in 3 parts:

a) arr\[l..i] elements less than pivot.

b) arr\[i+1..j-1] elements equal to pivot.

c) arr\[j..r] elements greater than pivot.

See [this](https://www.geeksforgeeks.org/3-way-quicksort/) for implementation.

### Quick Select

**Quick Select** is a selection algorithm to find the k-th smallest element in an unordered list.

The algorithm is similar to QuickSort. The difference is, instead of recurring for both sides (after finding pivot), it recurs only for the part that contains the k-th smallest element.

This reduces the expected complexity from O(n log n) to O(n), with a worst case of O(n^2).

**Pseudo Code:**

```java
function quickSelect(list, left, right, k)

   if left = right
      return list[left]

   Select a pivotIndex between left and right

   pivotIndex := partition(list, left, right, 
                                  pivotIndex)
   if k = pivotIndex
      return list[k]
   else if k < pivotIndex
      right := pivotIndex - 1
   else
      left := pivotIndex + 1
```

### **QuickSort vs MergeSort**

Source: [https://www.baeldung.com/java-quicksort](https://www.baeldung.com/java-quicksort)

Let’s discuss in which cases we should choose QuickSort over MergeSort.

Although both Quicksort and Mergesort have an average time complexity of _O(n log n)_, Quicksort is the preferred algorithm, as it has an \_O(log(n)) \_space complexity. Mergesort, on the other hand, requires \_O(n) \_extra storage, which makes it quite expensive for arrays.

Quicksort requires to access different indices for its operations, but this access is not directly possible in linked lists, as there are no continuous blocks; therefore to access an element we have to iterate through each node from the beginning of the linked list. Also, Mergesort is implemented without extra space for _LinkedLists._

In such case, overhead increases for Quicksort and Mergesort is generally preferred.

## Reference

[Toptal: Sorting Algorithms Animations](https://www.toptal.com/developers/sorting-algorithms)

Leetcode 排序类题目 排序算法总结: [https://www.jianshu.com/p/fb3e38defec4](broken-reference)
