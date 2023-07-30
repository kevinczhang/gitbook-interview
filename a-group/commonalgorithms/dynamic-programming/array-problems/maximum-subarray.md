# Maximum Subarray

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Example:**

```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

**Follow up:**

If you have figured out the O(_n_) solution, try coding another solution using the divide and conquer approach, which is more subtle.

```java
 /**     
  * @param nums: A list of integers
  * @return: A integer indicate the sum of max subarray
  */
 public int maxSubArray(int[] nums) {
   int localWithLast = nums[0], max = nums[0];
   for(int I = 1; I < nums.length; i++){
     localWithLast = Math.max(localWithLast + nums[i], nums[i]);
     max = Math.max(max, localWithLast);
   }
   return max;
}
```

