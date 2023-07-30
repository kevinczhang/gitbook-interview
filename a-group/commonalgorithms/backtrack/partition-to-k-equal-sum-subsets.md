# Partition to K Equal Sum Subsets



Given an integer array `nums` and an integer `k`, return `true` if it is possible to divide this array into `k` non-empty subsets whose sums are all equal.

&#x20;

**Example 1:**

<pre><code>Input: nums = [4,3,2,3,5,2,1], k = 4
<strong>Output:
</strong> true
<strong>Explanation:
</strong> It is possible to divide it into 4 subsets (5), (1, 4), (2,3), (2,3) with equal sums.
</code></pre>

**Example 2:**

<pre><code>Input: nums = [1,2,3,4], k = 3
<strong>Output:
</strong> false
</code></pre>

&#x20;

**Constraints:**

* `1 <= k <= nums.length <= 16`
* `1 <= nums[i] <= 104`
* The frequency of each element is in the range `[1, 4]`.

## Solution 1

```java
class Solution {
    public boolean canPartitionKSubsets(int[] nums, int k) {
	var sum = IntStream.of(nums).sum();
	if (sum % k != 0)
		return false;
	return canPartitionKSubsets(nums, k, 0, 0, sum / k, new boolean[nums.length]);
}

private boolean canPartitionKSubsets(int[] nums, int k, int start, int currentBucketSum, int targetBucketSum, boolean[] used) {
	if (k == 1)
		return true;
	if (currentBucketSum > targetBucketSum)
		return false;
	if (currentBucketSum == targetBucketSum)
		return canPartitionKSubsets(nums, k - 1, 0, 0, targetBucketSum, used);
	// for each choice
	for (var i = start; i < nums.length; i++) {
		if (used[i])
			continue;
		// choose
		used[i] = true;
		// explore
		if (canPartitionKSubsets(nums, k, i + 1, currentBucketSum + nums[i], targetBucketSum, used))
			return true;
		// un-choose
		used[i] = false;
	}
	return false;
}
}
```

## Solution 2

```java
class Solution {
    public boolean canPartitionKSubsets(int[] nums, int k) {
        // 排除一些基本情况
        if (k > nums.length) return false;
        int sum = 0;
        for (int v : nums) sum += v;
        if (sum % k != 0) return false;
        
        int used = 0; // 使用位图技巧
        int target = sum / k;
        // k 号桶初始什么都没装，从 nums[0] 开始做选择
        return backtrack(k, 0, nums, 0, used, target);
    }

    HashMap<Integer, Boolean> memo = new HashMap<>();

    boolean backtrack(int k, int bucket,
                    int[] nums, int start, int used, int target) {        
        // base case
        if (k == 0) {
            // 所有桶都被装满了，而且 nums 一定全部用完了
            return true;
        }
        if (bucket == target) {
            // 装满了当前桶，递归穷举下一个桶的选择
            // 让下一个桶从 nums[0] 开始选数字
            boolean res = backtrack(k - 1, 0, nums, 0, used, target);
            // 缓存结果
            memo.put(used, res);
            return res;
        }
        
        if (memo.containsKey(used)) {
            // 避免冗余计算
            return memo.get(used);
        }

        for (int i = start; i < nums.length; i++) {
            // 剪枝
            if (((used >> i) & 1) == 1) { // 判断第 i 位是否是 1
                // nums[i] 已经被装入别的桶中
                continue;
            }
            if (nums[i] + bucket > target) {
                continue;
            }
            // 做选择
            used |= 1 << i; // 将第 i 位置为 1
            bucket += nums[i];
            // 递归穷举下一个数字是否装入当前桶
            if (backtrack(k, bucket, nums, i + 1, used, target)) {
                return true;
            }
            // 撤销选择
            used ^= 1 << i; // 将第 i 位置为 0
            bucket -= nums[i];
        }

        return false;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=698

```
