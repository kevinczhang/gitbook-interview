# Minimum Path Sum



Given a `m x n` `grid` filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg)

<pre><code>Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
<strong>Output:
</strong> 7
<strong>Explanation:
</strong> Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.
</code></pre>

**Example 2:**

<pre><code>Input: grid = [[1,2,3],[4,5,6]]
<strong>Output:
</strong> 12
</code></pre>

&#x20;

**Constraints:**

* `m == grid.length`
* `n == grid[i].length`
* `1 <= m, n <= 200`
* `0 <= grid[i][j] <= 100`

## `Solution`

```java
class Solution {
    int[][] memo;

    public int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        // 构造备忘录，初始值全部设为 -1
        memo = new int[m][n];
        for (int[] row : memo)
            Arrays.fill(row, -1);

        return dp(grid, m - 1, n - 1);
    }

    int dp(int[][] grid, int i, int j) {
        // base case
        if (i == 0 && j == 0) {
            return grid[0][0];
        }
        if (i < 0 || j < 0) {
            return Integer.MAX_VALUE;
        }
        // 避免重复计算
        if (memo[i][j] != -1) {
            return memo[i][j];
        }
        // 将计算结果记入备忘录
        memo[i][j] = Math.min(
                dp(grid, i - 1, j),
                dp(grid, i, j - 1)
        ) + grid[i][j];

        return memo[i][j];
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=64

```
