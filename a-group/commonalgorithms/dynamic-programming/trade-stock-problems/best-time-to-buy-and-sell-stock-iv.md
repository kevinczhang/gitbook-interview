# Best Time to Buy and Sell Stock IV

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most **k** transactions.

**Note:**\
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

**Example 1:**

```
Input: [2,4,1], k = 2
Output: 2
Explanation: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.
```

**Example 2:**

```
Input: [3,2,6,5,0,3], k = 2
Output: 7
Explanation: Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4.
             Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
```

## Solution 0

```java
class Solution {
    public int maxProfit(int max_k, int[] prices) {
        int n = prices.length;
        if (n <= 0) {
            return 0;
        }
        if (max_k > n / 2) {
            // 交易次数 k 没有限制的情况
            return maxProfit_k_inf(prices);
        }

        // base case：
        // dp[-1][...][0] = dp[...][0][0] = 0
        // dp[-1][...][1] = dp[...][0][1] = -infinity
        int[][][] dp = new int[n][max_k + 1][2];
        // k = 0 时的 base case
        for (int i = 0; i < n; i++) {
            dp[i][0][1] = Integer.MIN_VALUE;
            dp[i][0][0] = 0;
        }

        for (int i = 0; i < n; i++)
            for (int k = max_k; k >= 1; k--) {
                if (i - 1 == -1) {
                    // 处理 i = -1 时的 base case
                    dp[i][k][0] = 0;
                    dp[i][k][1] = -prices[i];
                    continue;
                }
                // 状态转移方程
                dp[i][k][0] = Math.max(dp[i - 1][k][0], dp[i - 1][k][1] + prices[i]);
                dp[i][k][1] = Math.max(dp[i - 1][k][1], dp[i - 1][k - 1][0] - prices[i]);
            }
        return dp[n - 1][max_k][0];
    }

    // 第 122 题，k 无限的解法
    private int maxProfit_k_inf(int[] prices) {
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
// https://labuladong.github.io/article/?qno=188

```

## Solution 1

```java
public class Solution {
    public int maxProfit(int k, int[] prices) {
        if (prices.length < 2) return 0;        
        int days = prices.length;
        if (k >= days/2) return maxProfit2(prices);
        
        int[][] local = new int[days][k + 1];
        int[][] global = new int[days][k + 1];        
        for (int i = 1; i < days ; i++) {
            int diff = prices[i] - prices[i - 1];            
            for (int j = 1; j <= k; j++) {
                local[i][j] = Math.max(global[i - 1][j - 1], local[i - 1][j] + diff);
                global[i][j] = Math.max(global[i - 1][j], local[i][j]);
             }
        }        
        return global[days - 1][k];
    }    
    
    public int maxProfit2(int[] prices) {
        int maxProfit = 0;        
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) {
                maxProfit += prices[i] - prices[i - 1];
            }
        }        
        return maxProfit;
    }

}
```

## Solution 2

```java
public class Solution {
    public int maxProfit(int k, int[] prices) {
        if (prices.length < 2) return 0;
        if (k >= prices.length/2) return maxProfit2(prices);
        
        int[] local = new int[k + 1];
        int[] global = new int[k + 1];
        
        for (int i = 1; i < prices.length ; i++) {
            int diff = prices[i] - prices[i - 1];            
            for (int j = k; j > 0; j--) {
                local[j] = Math.max(global[j - 1], local[j] + diff);
                global[j] = Math.max(global[j], local[j]);
            }
        }        
        return global[k];
    }  
    
    public int maxProfit2(int[] prices) {
        int maxProfit = 0;        
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) {
                maxProfit += prices[i] - prices[i - 1];
            }
        }        
        return maxProfit;
    }

}
```
