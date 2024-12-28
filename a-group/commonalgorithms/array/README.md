---
description: Common algorithms for array
---

# Array and matrix

### Conversion between Array and ArrayList in Java

#### From `Array` to `ArrayList`

```java
// java.util.ArrayList

Element[] array = {new Element(1),new Element(2),new Element(3)};

// 1. Most popular and accepted answer
ArrayList<Element> arrayList = new ArrayList<Element>(Arrays.asList(array));

// Next popular answer
List<Element> list = Arrays.asList(array);
// Cons: It is not the best, because the size of the list returned from asList() is fixed
```

#### From `ArrayList` to `Array`:

[https://www.geeksforgeeks.org/arraylist-array-conversion-java-toarray-methods/](https://www.geeksforgeeks.org/arraylist-array-conversion-java-toarray-methods/)

[https://stackoverflow.com/questions/7969023/from-arraylist-to-array](https://stackoverflow.com/questions/7969023/from-arraylist-to-array)

```java
// Method 1: Using Object[] toArray() method


// (Preferred) Method 2: Using T[] toArray(T[] a)
// a − This is the array into which the elements of the list are to be stored, 
// if it is big enough; otherwise, a new array of the same runtime type is allocated for this purpose.
// java.util.ArrayList.toArray(T[])

ArrayList<Integer> foo = new ArrayList<Integer>();
foo.add(1);
foo.add(1);
foo.add(2);
foo.add(3);
foo.add(5);

Integer[] bar = foo.toArray(new Integer[foo.size()]);

System.out.println("bar.length = " + bar.length);


// Method 3: Using get() in for loop manually
```

[https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html)

The following from source: [https://docs.oracle.com/javase/tutorial/collections/interfaces/collection.html](https://docs.oracle.com/javase/tutorial/collections/interfaces/collection.html)

For example, suppose that`c`is a`Collection`. The following snippet dumps the contents of`c`into a newly allocated array of`Object`whose length is identical to the number of elements in`c`.

```
Object[] a = c.toArray();
```

Suppose that`c`is known to contain only strings (perhaps because`c`is of type`Collection<String>`). The following snippet dumps the contents of`c`into a newly allocated array of`String`whose length is identical to the number of elements in`c`.

```
String[] a = c.toArray(new String[0]);
```

### Sliding Window

A sliding window is an abstract concept commonly used in array/string problems. A window is a range of elements in the array/string which usually defined by the start and end indices, i.e. `[i,j)` (left-closed, right-open). A sliding window is a window "slides" its two boundaries to the certain direction. For example, if we slide `[i, j)`to the right by 11 element, then it becomes `[i+1, j+1)` (left-closed, right-open).

### **Prefix Sum**

Prefix sum 数组的 local / global 通用模板，求 min / max 皆可，使用时需要注意初始条件以及顺序:

```java
        int[] leftMax = new int[n];
        int prefixSum = 0;
        // 代表从起始位置开始，值最小的连续和数组
        int localMin = 0;
        int globalMax = Integer.MIN_VALUE;
        for(int i = 0; i < n; i++){
            prefixSum += nums[i];
            globalMax = Math.max(globalMax, prefixSum - localMin);
            localMin = Math.min(localMin, prefixSum);

            leftMax[i] = globalMax;
        }
```

### Kadane's Algorithm

Kadane's Algorithm 相比 prefix sum 的特点是，必须要以 nums\[0] 做初始化，从 index = 1 开始搜，优点是在处理 prefix product 的时候更容易处理好“-1” 和 “0” 的情况。

这类靠 prefix sum/product 的 subarray 问题，要注意好对于每一个子问题的 local / global 最优解结构，其中 local 解都是“以当前结尾 && 连续”，而 global 未必。

```java
public class Solution {
    public int maxSubArray(int[] nums) {
        if(nums == null || nums.length == 0) return 0;

        int localMax = nums[0];
        int globalMax = nums[0];
        for(int i = 1; i < nums.length; i++){
            localMax = Math.max(nums[i], localMax + nums[i]);
            globalMax = Math.max(globalMax, localMax);
        }

        return globalMax;
    }
}
```

\***Subarray Sum 系列问题参考：**

Source: [https://mnmunknown.gitbooks.io/algorithm-notes/626,\_dong\_tai\_gui\_hua\_ff0c\_subarray\_lei.html](https://mnmunknown.gitbooks.io/algorithm-notes/626,_dong_tai_gui_hua_ff0c_subarray_lei.html)
