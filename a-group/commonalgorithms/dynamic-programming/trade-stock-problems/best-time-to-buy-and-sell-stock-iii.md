# Best Time to Buy and Sell Stock III



You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

Find the maximum profit you can achieve. You may complete **at most two transactions**.

**Note:** You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

&#x20;

**Example 1:**

<pre><code>Input: prices = [3,3,5,0,0,3,1,4]
<strong>Output:
</strong> 6
<strong>Explanation:
</strong> Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
</code></pre>

**Example 2:**

<pre><code>Input: prices = [1,2,3,4,5]
<strong>Output:
</strong> 4
<strong>Explanation:
</strong> Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.
</code></pre>

**Example 3:**

<pre><code>Input: prices = [7,6,4,3,1]
<strong>Output:
</strong> 0
<strong>Explanation:
</strong> In this case, no transaction is done, i.e. max profit = 0.
</code></pre>

&#x20;

**Constraints:**

* `1 <= prices.length <= 105`
* `0 <= prices[i] <= 105`

## `Solution`

```java
class Solution {
    public int maxProfit(int[] prices) {
        int max_k = 2, n = prices.length;
        int[][][] dp = new int[n][max_k + 1][2];
        for (int i = 0; i < n; i++) {
            for (int k = max_k; k >= 1; k--) {
                if (i - 1 == -1) {
                    // 处理 base case
                    dp[i][k][0] = 0;
                    dp[i][k][1] = -prices[i];
                    continue;
                }
                dp[i][k][0] = Math.max(dp[i-1][k][0], dp[i-1][k][1] + prices[i]);
                dp[i][k][1] = Math.max(dp[i-1][k][1], dp[i-1][k-1][0] - prices[i]);
            }
        }
        // 穷举了 n × max_k × 2 个状态，正确。
        return dp[n - 1][max_k][0];
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=123

```
