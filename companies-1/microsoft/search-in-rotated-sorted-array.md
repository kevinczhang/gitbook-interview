# Search in Rotated Sorted Array

There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, `nums` is **possibly rotated** at an unknown pivot index `k` (`1 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the possible rotation and an integer `target`, return _the index of_ `target` _if it is in_ `nums`_, or_ `-1` _if it is not in_ `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

&#x20;

**Example 1:**

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

**Example 2:**

```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

**Example 3:**

```
Input: nums = [1], target = 0
Output: -1
```

&#x20;

**Constraints:**

* `1 <= nums.length <= 5000`
* `-104 <= nums[i] <= 104`
* All values of `nums` are **unique**.
* `nums` is an ascending array that is possibly rotated.
* `-104 <= target <= 104`

## Solution

```java
public class Solution {
    public int search(int[] A, int target) {
        // IMPORTANT: Please reset any member data you declared, as
        // the same Solution instance will be reused for each test case.
        int l = 0, r = A.length - 1;

	while (l <= r) {
		int m = l + (r - l) / 2;
		if (A[m] == target) 
			return m;
		if (A[l] <= A[m]) {
			if (target >= A[l] && target <= A[m])
				r = m;
			else
				l = m + 1;
		} else {
			if (target <= A[r] && target >= A[m])
				l = m;
			else
				r = m - 1;
		}
	}

	return -1;
    }
}
```
