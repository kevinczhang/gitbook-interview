# State Transition by Inaction

This is a small pattern that occasionally shows up in DP problems. Here, "doing nothing" refers to two different states having the same value. We're calling it "doing nothing" because often the way we arrive at a new state with the same value as the previous state is by "doing nothing" (we'll look at some examples soon). Of course, a decision making process needs to coexist with this pattern, because if we just had all states having the same value, the problem wouldn't really make sense (\text{dp(i) = dp(i - 1)} ?dp(i) = dp(i - 1)?) It is just that if we are trying to maximize or minimize a score for example, sometimes the best option is to "do nothing", which leads to two states having the same value. The actual recurrence relation would look something like \text{dp(i, j) = max(dp(i - 1, j), ...)}dp(i, j) = max(dp(i - 1, j), ...).

Usually when we "do nothing", it is by moving to the next element in some input array (which we usually use \text{i}i as a state variable for). As mentioned above, **this will be part of a decision making process due to some restriction in the problem**. For example, think back to House Robber: we could choose to rob or not rob each house we were at. Sometimes, not robbing the house is the best decision (because we aren't allowed to rob adjacent houses), then \text{dp(i) = dp(i - 1)}dp(i) = dp(i - 1).

## Example 188. Best Time to Buy and Sell Stock IV



> For this one, we're back to starting with top-down.

In this article, we'll be using the framework to solve [Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/). This problem is rated as "hard" and may seem daunting at first, but with the framework, the logic behind solving this problem is very intuitive. We'll also make use of the pattern of "doing nothing". Like usual, let's use the framework to develop an algorithm:

1\. A **function** that answers the problem for a given state

_What information do we need at each state/decision?_

We need to know what day it is (so we can look up the current price of the stock), and we need to know how many transactions we have left. These two are directly related to the input.

The note in the problem description says that we cannot engage in multiple transactions at the same time. This means that at any moment, we are either holding one unit of stock or not holding any stock. We should have a state variable that indicates if we are currently holding stock. This variable is fine as a boolean, but for caching purposes, let's use an integer alternating between \text{0}0 and \text{1}1 (\text{0}0 means not holding, \text{1}1 means holding).

To summarize, we have 3 state variables:

1. \text{i}i, which represents we are on the i^{th}ith day. The current price of the stock is \text{prices\[i]}prices\[i].
2. \text{transactionsRemaining}transactionsRemaining, which represents how many transactions we have left. This number goes down by 1 whenever we sell a stock.
3. \text{holding}holding, which is equal to \text{0}0 if we are not holding a stock, and \text{1}1 if we are holding a stock. If \text{holding}holding is \text{0}0, we have the option to buy a stock. Otherwise, we have the option to sell a stock.

The problem is asking for a maximum achievable profit. Therefore, let's have a function \text{dp}dp where \text{dp(i, transactionsRemaining, holding)}dp(i, transactionsRemaining, holding) returns the maximum achievable profit starting from the i^{th}ith day with \text{transactionsRemaining}transactionsRemaining transactions remaining, and \text{holding}holding indicating if we start with a stock or not. To answer the original problem, we would return \text{dp(0, k, 0)}dp(0, k, 0), as we start on day \text{0}0 with \text{k}k transactions remaining and not holding a stock.

2\. A **recurrence relation** to transition between states

At each state, we need to make a decision that depends on what \text{holding}holding is. Let's split it up and look at our options one at a time:

* If we are holding stock, we have two options. We can sell, or not sell. If we choose to sell, we gain \text{prices\[i]}prices\[i] money, and the next state will be \text{(i + 1, transactionsRemaining - 1, 0)}(i + 1, transactionsRemaining - 1, 0). This is because it is the next day (\text{i + 1}i + 1), we lose a transaction as we completed one by selling (\text{transactionsRemaining - 1}transactionsRemaining - 1), and we are no longer holding a stock (\text{0}0). In total, our profit is \text{prices\[i] + dp(i + 1, transactionsRemaining - 1, 0)}prices\[i] + dp(i + 1, transactionsRemaining - 1, 0). If we choose not to sell and **do nothing**, then we just move onto the next day with the same number of transactions, while still holding the stock. Our profit is \text{dp(i + 1, transactionsRemaining, holding)}dp(i + 1, transactionsRemaining, holding).
* If we are not holding stock, we have two options. We can buy, or not buy. If we choose to buy, we lose \text{prices\[i]}prices\[i] money, and the next state will be \text{(i + 1, transactionsRemaining, 1)}(i + 1, transactionsRemaining, 1). This is because it is the next day, we have the same number of transactions because transactions are only completed on selling, and we now hold a stock. In total, our profit is \text{-prices\[i] + dp(i + 1, transactionsRemaining, 1)}-prices\[i] + dp(i + 1, transactionsRemaining, 1). If we choose not to buy and **do nothing**, then we just move onto the next day with the same number of transactions, while still not having stock. Our profit is \text{dp(i + 1, transactionsRemaining, holding)}dp(i + 1, transactionsRemaining, holding).

> Note that you could also set up the solution so that transactions are completed upon buying a stock instead.

Of course, we always want to make the best decision. We can see that in both scenarios, **doing nothing** is the same - \text{dp(i + 1, transactionsRemaining, holding)}dp(i + 1, transactionsRemaining, holding). Therefore, we have a recurrence relation of:

`dp(i, transactionsRemaining, holding) = max(doNothing, sellStock)` if `holding == 1` otherwise `max(doNothing, buyStock)`

Where,\
`doNothing = dp(i + 1, transactionsRemaining, holding)`,\
`sellStock = prices[i] + dp(i + 1, transactionsRemaining - 1, 0)`, and\
`buyStock = -prices[i] + dp(i + 1, transactionsRemaining, 1)`.

![](https://leetcode.com/explore/learn/card/Figures/DP1/C3A5\_1.png)\


3\. **Base cases**

Both base cases are very simple for this problem. If we are out of transactions (\text{transactionsRemaining = 0}transactionsRemaining = 0), then we should immediately return \text{0}0 as we cannot make any more money. If the stock is no longer on the market (\text{i = prices.length}i = prices.length), then we should also return \text{0}0, as we cannot make any more money.

\


#### Top-down Implementation <a href="#top-down-implementation" id="top-down-implementation"></a>

```java
class Solution {
    private int[] prices;
    private int[][][] memo;
    
    private int dp(int i, int transactionsRemaining, int holding) {
        // Base cases
        if (transactionsRemaining == 0 || i == prices.length) {
            return 0;
        }
        
        if (memo[i][transactionsRemaining][holding] == 0) {
            int doNothing = dp(i + 1, transactionsRemaining, holding);
            int doSomething;

            if (holding == 1) {
                // Sell Stock
                doSomething = prices[i] + dp(i + 1, transactionsRemaining - 1, 0);
            } else {
                // Buy Stock
                doSomething = -prices[i] + dp(i + 1, transactionsRemaining, 1);
            }
            
            // Recurrence relation. Choose the most profitable option.
            memo[i][transactionsRemaining][holding] = Math.max(doNothing, doSomething);
        }
        
        return memo[i][transactionsRemaining][holding];
    }
    
    public int maxProfit(int k, int[] prices) {
        this.prices = prices;
        this.memo = new int[prices.length][k + 1][2];
        return dp(0, k, 0);
    }
}
```

#### Bottom-up Implementation <a href="#bottom-up-implementation" id="bottom-up-implementation"></a>

Again, the recurrence relation is the same with top-down, but we need to be careful about how we configure our for loops. The base cases are automatically handled because the \text{dp}dp array is initialized with all values set to \text{0}0. For iteration direction and order, remember with bottom-up we start at the base cases. Therefore we will start iterating from the end of the input and with only 1 transaction remaining.

```
class Solution {
    public int maxProfit(int k, int[] prices) {
        int n = prices.length;
        int dp[][][] = new int[n + 1][k + 1][2];
        
        for (int i = n - 1; i >= 0; i--) {
            for (int transactionsRemaining = 1; transactionsRemaining <= k; transactionsRemaining++) {
                for (int holding = 0; holding < 2; holding++) {
                    int doNothing = dp[i + 1][transactionsRemaining][holding];
                    int doSomething;
                    if (holding == 1) {
                        // Sell stock
                        doSomething = prices[i] + dp[i + 1][transactionsRemaining - 1][0];
                    } else {
                        // Buy stock
                        doSomething = -prices[i] + dp[i + 1][transactionsRemaining][1];
                    }
                    
                    // Recurrence relation
                    dp[i][transactionsRemaining][holding] = Math.max(doNothing, doSomething);
                }
            }
        }
        
        return dp[0][k][0];
    }
}
```

The time and space complexity of this problem for both implementations is the number of states since the recurrence relation is just a constant time formula. If \text{n = prices.length}n = prices.length, then this means the time and space complexity is O(n \cdot k \cdot 2) = O(n \cdot k)O(n⋅k⋅2)=O(n⋅k).
