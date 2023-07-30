# Maximum Product Subarray

Given an integer array `nums`, find the contiguous subarray within an array (containing at least one number) which has the largest product.

**Example 1:**

```
Input: [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```

**Example 2:**

```
Input: [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```

## Solution

```java
public class Solution {
    /**
     * @param nums: an array of integers
     * @return: an integer
     */
    public int maxProduct(int[] nums) {
          if (nums == null || nums.length == 0) return 0;
          if (nums.length == 1) return nums[0];
          int max_local = nums[0], min_local = nums[0], global = nums[0];
          for (int i = 1; i < nums.length; i++) {
		int max_copy = max_local;
		max_local = Math.max(Math.max(nums[i] * max_local, nums[i]), nums[i] * min_local);
		min_local = Math.min(Math.min(nums[i] * max_copy, nums[i]), nums[i] * min_local);
		global = Math.max(global, max_local);
	}
	return global;
    }
}

```
