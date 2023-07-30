# Minimum Falling Path Sum



Given an `n x n` array of integers `matrix`, return _the **minimum sum** of any **falling path** through_ `matrix`.

A **falling path** starts at any element in the first row and chooses the element in the next row that is either directly below or diagonally left/right. Specifically, the next element from position `(row, col)` will be `(row + 1, col - 1)`, `(row + 1, col)`, or `(row + 1, col + 1)`.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/11/03/failing1-grid.jpg)

<pre><code>Input: matrix = [[2,1,3],[6,5,4],[7,8,9]]
<strong>Output:
</strong> 13
<strong>Explanation:
</strong> There are two falling paths with a minimum sum as shown.
</code></pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/11/03/failing2-grid.jpg)

<pre><code>Input: matrix = [[-19,57],[-40,-5]]
<strong>Output:
</strong> -59
<strong>Explanation:
</strong> The falling path with a minimum sum is shown.
</code></pre>

&#x20;

**Constraints:**

* `n == matrix.length == matrix[i].length`
* `1 <= n <= 100`
* `-100 <= matrix[i][j] <= 100`

## `Solution`

```java
class Solution {
    public int minFallingPathSum(int[][] matrix) {
        int n = matrix.length;
        int res = Integer.MAX_VALUE;
        // 备忘录里的值初始化为 66666
        memo = new int[n][n];
        for (int i = 0; i < n; i++) {
            Arrays.fill(memo[i], 66666);
        }
        // 终点可能在 matrix[n-1] 的任意一列
        for (int j = 0; j < n; j++) {
            res = Math.min(res, dp(matrix, n - 1, j));
        }
        return res;
    }

    // 备忘录
    int[][] memo;

    int dp(int[][] matrix, int i, int j) {
        // 1、索引合法性检查
        if (i < 0 || j < 0 ||
                i >= matrix.length ||
                j >= matrix[0].length) {

            return 99999;
        }
        // 2、base case
        if (i == 0) {
            return matrix[0][j];
        }
        // 3、查找备忘录，防止重复计算
        if (memo[i][j] != 66666) {
            return memo[i][j];
        }
        // 进行状态转移
        memo[i][j] = matrix[i][j] + min(
                dp(matrix, i - 1, j),
                dp(matrix, i - 1, j - 1),
                dp(matrix, i - 1, j + 1)
        );

        return memo[i][j];
    }
    int min(int a, int b, int c) {
        return Math.min(a, Math.min(b, c));
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=931

```
