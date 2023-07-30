# Coin Change



You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return _the fewest number of coins that you need to make up that amount_. If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

&#x20;

**Example 1:**

<pre><code>Input: coins = [1,2,5], amount = 11
<strong>Output:
</strong> 3
<strong>Explanation:
</strong> 11 = 5 + 5 + 1
</code></pre>

**Example 2:**

<pre><code>Input: coins = [2], amount = 3
<strong>Output:
</strong> -1
</code></pre>

**Example 3:**

<pre><code>Input: coins = [1], amount = 0
<strong>Output:
</strong> 0
</code></pre>

&#x20;

**Constraints:**

* `1 <= coins.length <= 12`
* `1 <= coins[i] <= 231 - 1`
* `0 <= amount <= 104`

## `Solution`

```java
class Solution {
    int[] memo;

    public int coinChange(int[] coins, int amount) {
        memo = new int[amount + 1];
        // dp 数组全都初始化为特殊值
        Arrays.fill(memo, -666);
        return dp(coins, amount);
    }

    int dp(int[] coins, int amount) {
        if (amount == 0) return 0;
        if (amount < 0) return -1;
        // 查备忘录，防止重复计算
        if (memo[amount] != -666)
            return memo[amount];

        int res = Integer.MAX_VALUE;
        for (int coin : coins) {
            // 计算子问题的结果
            int subProblem = dp(coins, amount - coin);
            // 子问题无解则跳过
            if (subProblem == -1) continue;
            // 在子问题中选择最优解，然后加一
            res = Math.min(res, subProblem + 1);
        }
        // 把计算结果存入备忘录
        memo[amount] = (res == Integer.MAX_VALUE) ? -1 : res;
        return memo[amount];
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=322

```
