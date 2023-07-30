# Partition Equal Subset Sum



Given a **non-empty** array `nums` containing **only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

&#x20;

**Example 1:**

<pre><code>Input: nums = [1,5,11,5]
<strong>Output:
</strong> true
<strong>Explanation:
</strong> The array can be partitioned as [1, 5, 5] and [11].
</code></pre>

**Example 2:**

<pre><code>Input: nums = [1,2,3,5]
<strong>Output:
</strong> false
<strong>Explanation:
</strong> The array cannot be partitioned into equal sum subsets.
</code></pre>

&#x20;

**Constraints:**

* `1 <= nums.length <= 200`
* `1 <= nums[i] <= 100`

## `Solution`

```java
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for (int num : nums) sum += num;
        // 和为奇数时，不可能划分成两个和相等的集合
        if (sum % 2 != 0) return false;
        int n = nums.length;
        sum = sum / 2;
        boolean[][] dp = new boolean[n + 1][sum + 1];
        // base case
        for (int i = 0; i <= n; i++)
            dp[i][0] = true;

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= sum; j++) {
                if (j - nums[i - 1] < 0) {
                    // 背包容量不足，不能装入第 i 个物品
                    dp[i][j] = dp[i - 1][j];
                } else {
                    // 装入或不装入背包
                    dp[i][j] = dp[i - 1][j] || dp[i - 1][j - nums[i - 1]];
                }
            }
        }
        return dp[n][sum];
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=416

```
