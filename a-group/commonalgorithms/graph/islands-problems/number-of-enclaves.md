# Number of Enclaves



You are given an `m x n` binary matrix `grid`, where `0` represents a sea cell and `1` represents a land cell.

A **move** consists of walking from one land cell to another adjacent (**4-directionally**) land cell or walking off the boundary of the `grid`.

Return _the number of land cells in_ `grid` _for which we cannot walk off the boundary of the grid in any number of **moves**_.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/18/enclaves1.jpg)

<pre><code>Input: grid = [[0,0,0,0],[1,0,1,0],[0,1,1,0],[0,0,0,0]]
<strong>Output:
</strong> 3
<strong>Explanation:
</strong> There are three 1s that are enclosed by 0s, and one 1 that is not enclosed because its on the boundary.
</code></pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/18/enclaves2.jpg)

<pre><code>Input: grid = [[0,1,1,0],[0,0,1,0],[0,0,1,0],[0,0,0,0]]
<strong>Output:
</strong> 0
<strong>Explanation:
</strong> All 1s are either on the boundary or can reach the boundary.
</code></pre>

&#x20;

**Constraints:**

* `m == grid.length`
* `n == grid[i].length`
* `1 <= m, n <= 500`
* `grid[i][j]` is either `0` or `1`.

## Solution

```java
class Solution {
    public int numEnclaves(int[][] grid) {
        int m = grid.length, n = grid[0].length;

        for (int i = 0; i < m; i++) {
            dfs(grid, i, 0);
            dfs(grid, i, n - 1);
        }

        for (int j = 0; j < n; j++) {
            dfs(grid, 0, j);
            dfs(grid, m - 1, j);
        }

        int res = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) {
                    res += 1;
                }
            }
        }
        return res;
    }

    void dfs(int[][] grid, int i, int j) {
        int m = grid.length, n = grid[0].length;
        if (i < 0 || j < 0 || i >= m || j >= n || grid[i][j] == 0) {
            return;
        }

        grid[i][j] = 0;

        dfs(grid, i + 1, j);
        dfs(grid, i, j + 1);
        dfs(grid, i - 1, j);
        dfs(grid, i, j - 1);
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=1020

```
