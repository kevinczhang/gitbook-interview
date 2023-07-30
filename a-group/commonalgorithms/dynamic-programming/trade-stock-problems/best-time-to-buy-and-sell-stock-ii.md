# Best Time to Buy and Sell Stock II



You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

On each day, you may decide to buy and/or sell the stock. You can only hold **at most one** share of the stock at any time. However, you can buy it then immediately sell it on the **same day**.

Find and return _the **maximum** profit you can achieve_.

&#x20;

**Example 1:**

<pre><code>Input: prices = [7,1,5,3,6,4]
<strong>Output:
</strong> 7
<strong>Explanation:
</strong> Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Total profit is 4 + 3 = 7.
</code></pre>

**Example 2:**

<pre><code>Input: prices = [1,2,3,4,5]
<strong>Output:
</strong> 4
<strong>Explanation:
</strong> Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Total profit is 4.
</code></pre>

**Example 3:**

<pre><code>Input: prices = [7,6,4,3,1]
<strong>Output:
</strong> 0
<strong>Explanation:
</strong> There is no way to make a positive profit, so we never buy the stock to achieve the maximum profit of 0.
</code></pre>

&#x20;

**Constraints:**

* `1 <= prices.length <= 3 * 104`
* `0 <= prices[i] <= 104`

## `Solution`

```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int[][] dp = new int[n][2];
        for (int i = 0; i < n; i++) {
            if (i - 1 == -1) {
                // base case
                dp[i][0] = 0;
                dp[i][1] = -prices[i];
                continue;
            }
            dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1] + prices[i]);
            dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] - prices[i]);
        }
        return dp[n - 1][0];
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=122

```
