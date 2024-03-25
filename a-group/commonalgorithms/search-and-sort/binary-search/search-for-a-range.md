---
description: >-
  https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/
---

# Search for a Range

Given an array of integers `nums` sorted in ascending order, find the starting and ending position of a given `target` value.

Your algorithm's runtime complexity must be in the order of _O_(log _n_).

If the target is not found in the array, return `[-1, -1]`.

**Example 1:**

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

**Example 2:**

```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

```java
public class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] res = new int[]{-1, -1};
        if (nums.length == 0)
            return res;        
        res[0] = searchLow(nums, target);
        if (res[0]> -1){
            res[1] = searchHigh(nums, target);            
        }
        return res;
    }
    
    private int searchLow(int[] nums, int target){
        int start = 0, end = nums.length - 1, mid;
        while (start <= end){
            mid = start + (end - start)/2;
            if (nums[mid] < target){
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        return (start < nums.length && target == nums[start]) ? start : -1;
    }
    
    private int searchHigh(int[] nums, int target){
        int start = 0, end = nums.length - 1, mid;
        while (start <= end){
            mid = start + (end - start)/2;
            if (nums[mid] > target){
                end = mid - 1;
            } else {                
                start = mid + 1;
            }
        }
        return (end >= 0 && target == nums[end]) ? end : -1;
    }
}
```
