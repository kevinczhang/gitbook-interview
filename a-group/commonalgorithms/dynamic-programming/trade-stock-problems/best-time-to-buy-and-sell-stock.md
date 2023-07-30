# Best Time to Buy and Sell Stock



You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return _the maximum profit you can achieve from this transaction_. If you cannot achieve any profit, return `0`.

&#x20;

**Example 1:**

<pre><code>Input: prices = [7,1,5,3,6,4]
<strong>Output:
</strong> 5
<strong>Explanation:
</strong> Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
</code></pre>

**Example 2:**

<pre><code>Input: prices = [7,6,4,3,1]
<strong>Output:
</strong> 0
<strong>Explanation:
</strong> In this case, no transactions are done and the max profit = 0.
</code></pre>

&#x20;

**Constraints:**

* `1 <= prices.length <= 105`
* `0 <= prices[i] <= 104`

## `Solution 1`

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length <= 1)
            return 0;
        int buyDay = 0, sellDay = 1, res = 0;
        while (sellDay < prices.length) {
            if (prices[sellDay] < prices[buyDay]) {
                buyDay = sellDay;
            } else {
                res = Math.max(res, prices[sellDay] - prices[buyDay]);
            }
            sellDay++;
        }
        return res;
    }
}
```

## `Solution 2`

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
            dp[i][1] = Math.max(dp[i - 1][1], -prices[i]);
        }
        return dp[n - 1][0];
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=121

```
