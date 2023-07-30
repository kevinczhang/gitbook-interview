# Coin Change 2



You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return _the number of combinations that make up that amount_. If that amount of money cannot be made up by any combination of the coins, return `0`.

You may assume that you have an infinite number of each kind of coin.

The answer is **guaranteed** to fit into a signed **32-bit** integer.

&#x20;

**Example 1:**

<pre><code>Input: amount = 5, coins = [1,2,5]
<strong>Output:
</strong> 4
<strong>Explanation:
</strong> there are four ways to make up the amount:
5=5
5=2+2+1
5=2+1+1+1
5=1+1+1+1+1
</code></pre>

**Example 2:**

<pre><code>Input: amount = 3, coins = [2]
<strong>Output:
</strong> 0
<strong>Explanation:
</strong> the amount of 3 cannot be made up just with coins of 2.
</code></pre>

**Example 3:**

<pre><code>Input: amount = 10, coins = [10]
<strong>Output:
</strong> 1
</code></pre>

&#x20;

**Constraints:**

* `1 <= coins.length <= 300`
* `1 <= coins[i] <= 5000`
* All the values of `coins` are **unique**.
* `0 <= amount <= 5000`

## `Solution`

```java
class Solution {
    public int change(int amount, int[] coins) {
        int n = coins.length;
        int[][] dp = new int[n + 1][amount + 1];
        // base case
        for (int i = 0; i <= n; i++)
            dp[i][0] = 1;

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= amount; j++)
                if (j - coins[i-1] >= 0)
                    dp[i][j] = dp[i - 1][j]
                            + dp[i][j - coins[i-1]];
                else
                    dp[i][j] = dp[i - 1][j];
        }
        return dp[n][amount];
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=518

```
