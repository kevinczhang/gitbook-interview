---
description: Leetcode 215
---

# Kth Largest Element in an Array



Given an integer array `nums` and an integer `k`, return _the_ `kth` _largest element in the array_.

Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

&#x20;

**Example 1:**

```
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
```

**Example 2:**

```
Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
```

&#x20;

**Constraints:**

* `1 <= k <= nums.length <= 104`
* `-104 <= nums[i] <= 104`

## Solution

```java
class Solution {
    int [] nums;

    public void swap(int a, int b) {
      int tmp = this.nums[a];
      this.nums[a] = this.nums[b];
      this.nums[b] = tmp;
    }

    public int partition(int left, int right, int pivot_index) {
      int pivot = this.nums[pivot_index];
      // 1. move pivot to end
      swap(pivot_index, right);
      int store_index = left;
  
      // 2. move all smaller elements to the left
      for (int i = left; i <= right; i++) {
        if (this.nums[i] < pivot) {
          swap(store_index, i);
          store_index++;
        }
      }
  
      // 3. move pivot to its final place
      swap(store_index, right);
  
      return store_index;
    }

    public int quickselect(int left, int right, int k_smallest) {      
      // Returns the k-th smallest element of list within left..right.  
      if (left == right) // If the list contains only one element,
        return this.nums[left];  // return that element
  
      // select a random pivot_index
      Random random_num = new Random();
      int pivot_index = left + random_num.nextInt(right - left);   
      pivot_index = partition(left, right, pivot_index);
  
      // the pivot is on (N - k)th smallest position
      if (k_smallest == pivot_index)
        return this.nums[k_smallest];
      // go left side
      else if (k_smallest < pivot_index)
        return quickselect(left, pivot_index - 1, k_smallest);
      // go right side
      return quickselect(pivot_index + 1, right, k_smallest);
    }
  
    public int findKthLargest(int[] nums, int k) {
      this.nums = nums;
      int size = nums.length;
      // kth largest is (N - k)th smallest
      return quickselect(0, size - 1, size - k);
    }
}
```
