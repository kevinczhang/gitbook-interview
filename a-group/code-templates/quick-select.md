# Quick select

## Top K Frequent Elements

Given an integer array `nums` and an integer `k`, return _the_ `k` _most frequent elements_. You may return the answer in **any order**.

&#x20;

**Example 1:**

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

**Example 2:**

```
Input: nums = [1], k = 1
Output: [1]
```

&#x20;

**Constraints:**

* `1 <= nums.length <= 105`
* `k` is in the range `[1, the number of unique elements in the array]`.
* It is **guaranteed** that the answer is **unique**.

&#x20;

**Follow up:** Your algorithm's time complexity must be better than `O(n log n)`, where n is the array's size.

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> numCounts = new HashMap<>();
        
        for (int i = 0; i < nums.length; i++) {
            numCounts.put(nums[i], numCounts.getOrDefault(nums[i], 0) + 1);
        }
        
        int[] uniquNums = new int[numCounts.size()];
        int i = 0;
        for (Integer key : numCounts.keySet()) {
            uniquNums[i++] = key;
        }
        
        return findKMostFrequent(uniquNums, numCounts, k);
    }
    
    private int[] findKMostFrequent(int[] nums, Map<Integer, Integer> numCounts, int k) {
        int left = 0, right = nums.length - 1;
        while (left < right) {
            int pivotInd = partition(nums, left, right, numCounts);
            if (pivotInd == k)
                return Arrays.copyOf(nums, k);
            if (pivotInd > k) {
                right = pivotInd - 1;
            } else {
                left = pivotInd + 1;
            }
        }
        return Arrays.copyOf(nums, k);
    }
    
    private int partition(int[] nums, int left, int right, Map<Integer, Integer> numCounts){
        Random rd = new Random();
        int pivotInd = left + rd.nextInt(right - left + 1);
        int pivot = numCounts.get(nums[pivotInd]);
        swap(nums, pivotInd, right);
        pivotInd = left;
        for (int i = left; i < right; i++) {
            if (numCounts.get(nums[i]) > pivot) {
                swap(nums, i, pivotInd++);
            }
        }
        swap(nums, pivotInd, right);
        return pivotInd;
    }
    
    private void swap(int[] nums, int n1, int n2){
        int temp = nums[n1];
        nums[n1] = nums[n2];
        nums[n2] = temp;
    }

```
