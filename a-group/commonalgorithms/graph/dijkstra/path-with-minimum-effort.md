# Path With Minimum Effort



You are a hiker preparing for an upcoming hike. You are given `heights`, a 2D array of size `rows x columns`, where `heights[row][col]` represents the height of cell `(row, col)`. You are situated in the top-left cell, `(0, 0)`, and you hope to travel to the bottom-right cell, `(rows-1, columns-1)` (i.e., **0-indexed**). You can move **up**, **down**, **left**, or **right**, and you wish to find a route that requires the minimum **effort**.

A route's **effort** is the **maximum absolute difference** in heights between two consecutive cells of the route.

Return _the minimum **effort** required to travel from the top-left cell to the bottom-right cell._

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/04/ex1.png)

<pre><code>Input: heights = [[1,2,2],[3,8,2],[5,3,5]]
<strong>Output:
</strong> 2
<strong>Explanation:
</strong> The route of [1,3,5,3,5] has a maximum absolute difference of 2 in consecutive cells.
This is better than the route of [1,2,2,2,5], where the maximum absolute difference is 3.
</code></pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/04/ex2.png)

<pre><code>Input: heights = [[1,2,3],[3,8,4],[5,3,5]]
<strong>Output:
</strong> 1
<strong>Explanation:
</strong> The route of [1,2,3,4,5] has a maximum absolute difference of 1 in consecutive cells, which is better than route [1,3,5,3,5].
</code></pre>

**Example 3:**

![](https://assets.leetcode.com/uploads/2020/10/04/ex3.png)

<pre><code>Input: heights = [[1,2,1,1,1],[1,2,1,2,1],[1,2,1,2,1],[1,2,1,2,1],[1,1,1,2,1]]
<strong>Output:
</strong> 0
<strong>Explanation:
</strong> This route does not require any effort.
</code></pre>

&#x20;

**Constraints:**

* `rows == heights.length`
* `columns == heights[i].length`
* `1 <= rows, columns <= 100`
* `1 <= heights[i][j] <= 106`

```java
class Solution {
    // Dijkstra 算法，计算 (0, 0) 到 (m - 1, n - 1) 的最⼩体⼒消耗
    public int minimumEffortPath(int[][] heights) {
        int m = heights.length, n = heights[0].length;
        // 定义：从 (0, 0) 到 (i, j) 的最⼩体⼒消耗是 effortTo[i][j]
        int[][] effortTo = new int[m][n];
        // dp table 初始化为正⽆穷
        for (int i = 0; i < m; i++) {
            Arrays.fill(effortTo[i], Integer.MAX_VALUE);
        }
        // base case，起点到起点的最⼩消耗就是 0
        effortTo[0][0] = 0;
        // 优先级队列，effortFromStart 较⼩的排在前⾯
        Queue<State> pq = new PriorityQueue<>((a, b) -> {
            return a.effortFromStart - b.effortFromStart;
        });
        // 从起点 (0, 0) 开始进⾏ BFS
        pq.offer(new State(0, 0, 0));
        while (!pq.isEmpty()) {
            State curState = pq.poll();
            int curX = curState.x;
            int curY = curState.y;
            int curEffortFromStart = curState.effortFromStart;
            // 到达终点提前结束
            if (curX == m - 1 && curY == n - 1) {
                return curEffortFromStart;
            }
            if (curEffortFromStart > effortTo[curX][curY]) {
                continue;
            }
            // 将 (curX, curY) 的相邻坐标装⼊队列
            for (int[] neighbor : adj(heights, curX, curY)) {
                int nextX = neighbor[0];
                int nextY = neighbor[1];
                // 计算从 (curX, curY) 达到 (nextX, nextY) 的消耗
                int effortToNextNode = Math.max(
                    effortTo[curX][curY],
                    Math.abs(heights[curX][curY] - heights[nextX][nextY])
                );
                // 更新 dp table
                if (effortTo[nextX][nextY] > effortToNextNode) {
                    effortTo[nextX][nextY] = effortToNextNode;
                    pq.offer(new State(nextX, nextY, effortToNextNode));
                }
            }
        }
        // 正常情况不会达到这个 return
        return -1;
    }
    
    // ⽅向数组，上下左右的坐标偏移量
    int[][] dirs = new int[][]{{0,1}, {1,0}, {0,-1}, {-1,0}};
    // 返回坐标 (x, y) 的上下左右相邻坐标
    List<int[]> adj(int[][] matrix, int x, int y) {
        int m = matrix.length, n = matrix[0].length;
        // 存储相邻节点
        List<int[]> neighbors = new ArrayList<>();
        for (int[] dir : dirs) {
            int nx = x + dir[0];
            int ny = y + dir[1];
            if (nx >= m || nx < 0 || ny >= n || ny < 0) {
                // 索引越界
                continue;
            }
            neighbors.add(new int[]{nx, ny});
        }
        return neighbors;
    }
}

class State {
    // 矩阵中的⼀个位置
    int x, y;
    // 从起点 (0, 0) 到当前位置的最⼩体⼒消耗（距离）
    int effortFromStart;
    State(int x, int y, int effortFromStart) {
        this.x = x;
        this.y = y;
        this.effortFromStart = effortFromStart;
    }
}
```
