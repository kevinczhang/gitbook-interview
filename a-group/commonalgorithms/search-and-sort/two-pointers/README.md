# Two pointers

## **Summary**

```
 两个指针
• 对撞型 (2 sum 类 和 partition 类)
• 前向型 (窗口类, 快慢类)
• 两个数组,两个指针 (并行)
```

```
模板
• 2 Sum类模板
• Partition 类模板
• 窗口类模板
```

## 1. “对撞型”或“相会型”

### Two Sum类题目思路

```java
if (A[i] + A[j] > sum)
    j--;
    do something
else if (A[i] + A[j] < sum)
    i++;
    do something
else
    do something
    i++ or j--
```

### 灌水类型题目思路

```java
if (A[i] > A[j])
    j--
else if (A[i] < A[j])
    i++
else
    i++ or j--
```

> 这一类通过对撞型指针优化算法，根本上其实要证明就是不用扫描多余状态

```java
// Give an array arr[]
int left = 0;
int right = arr.length - 1;

while(left < right) {
    if(arr[left] 和 arr[right] 满足某一条件) {
        // Do something
        right --; // 不用考虑[left + 1, right - 1] 和 right 组成的pair
    } else if (arr[left] 和 arr[right] 不满足某一条件) {
        left ++; // 不用考虑[left + 1, right - 1] 和 left 组成的pair
    }
}
```

### Partition类模板

```java
public int partition(int[] nums, int l, int r) {
    // 初始化左右指针和pivot
    int left = l, right = r;
    int pivot = nums[left];

    // 进行 partition
    while (left < right) {
        while (left < right && nums[right] >= pivot) {
            right--;
        }
        nums[left] = nums[right];
        while (left < right && nums[left] <= pivot) {
            left++;
        }
        nums[right] == nums[left];
    }

    // 返还pivot点到数组里
    nums[left] = pivot;
    return left;
}
```

#### Partition 另一种模板

```java
public void swap(int[] nums, int x, int y) {
    int tmp = nums[x];
    nums[x] = nums[y];
    nums[y] = tmp;
}

public int partition(int[] nums, int left, int right) {

    Random rand = new Random();
    int pivotIndex = rand.nextInt((right - left) + 1) + left;
    // Init pivot
    int pivotValue = nums[pivotIndex];

    swap(nums, pivotIndex, right);

    // First index that nums[firstIndex] > pivotValue
    int firstIndex = left;

    for (int i = left; i <= right - 1; i++) {
        if (nums[i] < pivotValue) {
            swap(nums, firstIndex, i);
            firstIndex++;
        }
    }

    // Recover pivot to array
    swap(nums, right, firstIndex);
    return firstIndex;
}
```

* [RosettaCode: Quickselect Algorithm](https://rosettacode.org/wiki/Quickselect\_algorithm#Java)
* [Code Scream: The Partition Algorithm - Used For Quick-Select and Quick-Sort](http://www.codescream.com/ContentDisplay?targetContent=Partition)
* [GeekViewpoint: Quickselect: Kth Greatest Value ](http://www.geekviewpoint.com/java/search/quickselect)
* [被忽视的 partition 算法](http://selfboot.cn/2016/09/01/lost\_partition/)

### 相会型指针题目

* 2 Sum 类 （通过判断条件优化算法）
  * 3 Sum Closest
  * 4 Sum
  * 3 Sum
  * Two sum II
  * Triangle Count
  * Trapping Rain Water
  * Container With Most Water
* Partition 类
  * Partition-array
  * Sort Colors
  * Partition Array by Odd and Even  &#x20;
  * Sort Letters by Case
  * Valid Palindrome
  * quick sort\\/ quick select\\/ nuts bolts problem\\/wiggle sort II

## 2. 前向型或者追击型

### 窗口类

窗口类指针移动模板

> 通过两层`for`循环改进算法 --- 不同于sliding window

```
优化类型:

* 优化思想通过两层for循环而来
* 外层指针依然是依次遍历
* 内层指针证明是否需要回退
```

```java
for (i = 0; i < n; i++) {
    while (j < n) {
        if (满足条件)
            j++
            更行j状态
        else (不满足条件)
            break
    }
    更新i状态
}
```

### 快慢类

```java
ListNode fast, slow;
fast = head.next;
slow = head;
while (fast != slow) {
    if(fast==null || fast.next==null)
        return false;
    fast = fast.next.next;
    slow = slow.next;
}
return true;
```

### 前向型指针题目

* 窗口类
  * Remove Nth Node From End of List
  * minimum-size-subarray-sum
  * Minimum Window Substring
  * Longest Substring with At Most K Distinct Characters
  * Longest Substring Without Repeating Characters
  * Longest Repeating Character Replacement
* 快慢类
  * Find the Middle of Linked L

## 两个数组两个指针

两个数组各找一个元素, 使得和等于target

1. 找一种
2. 找全部种类

From @LeetCode

## Two-pointer Technique - Scenario I (相会型)

One of the typical scenarios to use two-pointer technique is you want to:

> Iterate the array from two ends to the middle.

So that you can use the two-pointer technique:

> **One pointer starts from the beginning while the other pointer starts from the end.**

_**This technique is often used in a**_ `sorted` _**array.**_

## Two-pointer Technique - Scenario II （快慢型）

`two pointers with different steps` to solve problems.

Scenario:

> One slow-runner and one fast-runner at the same time.

The key to solving this kind of problems is to

> Determine the movement strategy for both pointers.

Similar to the previous scenario, you might sometimes need to `sort` the array before using the two-pointer technique. And you might need a `greedy` thought to determine your movement strategy.

应用场景

Two Pointer Technique can be used to solve:

* [Slow-pointer and fast-pointer problem in Linked List](https://leetcode.com/explore/learn/card/linked-list/214/linked-list-two-pointer/)
* Sliding Window Problem

### Sliding Window Problem

[904.Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)

[424.Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)
