# Target Sum



You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

* For example, if `nums = [2, 1]`, you can add a `'+'` before `2` and a `'-'` before `1` and concatenate them to build the expression `"+2-1"`.

Return the number of different **expressions** that you can build, which evaluates to `target`.

&#x20;

**Example 1:**

<pre><code>Input: nums = [1,1,1,1,1], target = 3
<strong>Output:
</strong> 5
<strong>Explanation:
</strong> There are 5 ways to assign symbols to make the sum of nums be target 3.
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3
</code></pre>

**Example 2:**

<pre><code>Input: nums = [1], target = 1
<strong>Output:
</strong> 1
</code></pre>

&#x20;

**Constraints:**

* `1 <= nums.length <= 20`
* `0 <= nums[i] <= 1000`
* `0 <= sum(nums[i]) <= 1000`
* `-1000 <= target <= 1000`

## `Solution`

```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        if (nums.length == 0) return 0;
        return dp(nums, 0, target);
    }

    // 备忘录
    HashMap<String, Integer> memo = new HashMap<>();

    int dp(int[] nums, int i, int remain) {
        // base case
        if (i == nums.length) {
            if (remain == 0) return 1;
            return 0;
        }
        // 把它俩转成字符串才能作为哈希表的键
        String key = i + "," + remain;
        // 避免重复计算
        if (memo.containsKey(key)) {
            return memo.get(key);
        }
        // 还是穷举
        int result = dp(nums, i + 1, remain - nums[i]) + dp(nums, i + 1, remain + nums[i]);
        // 记入备忘录
        memo.put(key, result);
        return result;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=494

```
