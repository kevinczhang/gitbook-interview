# Number of Closed Islands



Given a 2D `grid` consists of `0s` (land) and `1s` (water).  An _island_ is a maximal 4-directionally connected group of `0s` and a _closed island_ is an island **totally** (all left, top, right, bottom) surrounded by `1s.`

Return the number of _closed islands_.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/10/31/sample\_3\_1610.png)

<pre><code>Input: grid = [[1,1,1,1,1,1,1,0],[1,0,0,0,0,1,1,0],[1,0,1,0,1,1,1,0],[1,0,0,0,0,1,0,1],[1,1,1,1,1,1,1,0]]
<strong>Output:
</strong> 2
<strong>Explanation:
</strong> 
Islands in gray are closed because they are completely surrounded by water (group of 1s).
</code></pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/10/31/sample\_4\_1610.png)

<pre><code>Input: grid = [[0,0,1,0,0],[0,1,0,1,0],[0,1,1,1,0]]
<strong>Output:
</strong> 1
</code></pre>

**Example 3:**

<pre><code>Input: grid = [[1,1,1,1,1,1,1],
               [1,0,0,0,0,0,1],
               [1,0,1,1,1,0,1],
               [1,0,1,0,1,0,1],
               [1,0,1,1,1,0,1],
               [1,0,0,0,0,0,1],
               [1,1,1,1,1,1,1]]
<strong>Output:
</strong> 2
</code></pre>

&#x20;

**Constraints:**

* `1 <= grid.length, grid[0].length <= 100`
* `0 <= grid[i][j] <=1`

## `Solution`

```java
class Solution {
     // 主函数：计算封闭岛屿的数量
    public int closedIsland(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        for (int j = 0; j < n; j++) {
            // 把靠上边的岛屿淹掉
            dfs(grid, 0, j);
            // 把靠下边的岛屿淹掉
            dfs(grid, m - 1, j);
        }
        for (int i = 0; i < m; i++) {
            // 把靠左边的岛屿淹掉
            dfs(grid, i, 0);
            // 把靠右边的岛屿淹掉
            dfs(grid, i, n - 1);
        }
        // 遍历 grid，剩下的岛屿都是封闭岛屿
        int res = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 0) {
                    res++;
                    dfs(grid, i, j);
                }
            }
        }
        return res;
    }

    // 从 (i, j) 开始，将与之相邻的陆地都变成海水
    void dfs(int[][] grid, int i, int j) {
        int m = grid.length, n = grid[0].length;
        if (i < 0 || j < 0 || i >= m || j >= n) {
            return;
        }
        if (grid[i][j] == 1) {
            // 已经是海水了
            return;
        }
        // 将 (i, j) 变成海水
        grid[i][j] = 1;
        // 淹没上下左右的陆地
        dfs(grid, i + 1, j);
        dfs(grid, i, j + 1);
        dfs(grid, i - 1, j);
        dfs(grid, i, j - 1);
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=1254

```
