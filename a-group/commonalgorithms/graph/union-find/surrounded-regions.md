# Surrounded Regions



Given an `m x n` matrix `board` containing `'X'` and `'O'`, _capture all regions that are 4-directionally surrounded by_ `'X'`.

A region is **captured** by flipping all `'O'`s into `'X'`s in that surrounded region.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg)

<pre><code>Input: board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
<strong>Output:
</strong> [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
<strong>Explanation:
</strong> Notice that an 'O' should not be flipped if:
- It is on the border, or
- It is adjacent to an 'O' that should not be flipped.
The bottom 'O' is on the border, so it is not flipped.
The other three 'O' form a surrounded region, so they are flipped.
</code></pre>

**Example 2:**

<pre><code>Input: board = [["X"]]
<strong>Output:
</strong> [["X"]]
</code></pre>

&#x20;

**Constraints:**

* `m == board.length`
* `n == board[i].length`
* `1 <= m, n <= 200`
* `board[i][j]` is `'X'` or `'O'`.

```java
class Solution {
    public void solve(char[][] board) {
        if (board.length == 0) 
            return;
        int m = board.length;
        int n = board[0].length;
        // 给 dummy 留⼀个额外位置
        UF uf = new UF(m * n + 1);
        int dummy = m * n;
        // 将⾸列和末列的 O 与 dummy 连通
        for (int i = 0; i < m; i++) {
            if (board[i][0] == 'O')
            uf.union(i * n, dummy);
            if (board[i][n - 1] == 'O')
            uf.union(i * n + n - 1, dummy);
        }
        // 将⾸⾏和末⾏的 O 与 dummy 连通
        for (int j = 0; j < n; j++) {
            if (board[0][j] == 'O')
                uf.union(j, dummy);
            if (board[m - 1][j] == 'O')
                uf.union(n * (m - 1) + j, dummy);
        }
        // ⽅向数组 d 是上下左右搜索的常⽤⼿法
        int[][] d = new int[][]{{1,0}, {0,1}, {0,-1}, {-1,0}};
        for (int i = 1; i < m - 1; i++)
            for (int j = 1; j < n - 1; j++)
                if (board[i][j] == 'O')
                    // 将此 O 与上下左右的 O 连通
                    for (int k = 0; k < 4; k++) {
                        int x = i + d[k][0];
                        int y = j + d[k][1];
                        if (board[x][y] == 'O')
                        uf.union(x * n + y, i * n + j);
                    }
        
        // 所有不和 dummy 连通的 O，都要被替换
        for (int i = 1; i < m - 1; i++)
            for (int j = 1; j < n - 1; j++)
                if (!uf.connected(dummy, i * n + j))
                    board[i][j] = 'X';
    }
}

class UF {
    // 连通分量个数
    private int count;
    // 存储每个节点的⽗节点
    private int[] parent;
    
    // n 为图中节点的个数
    public UF(int n) {
        this.count = n;
        parent = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }
    
    // 将节点 p 和节点 q 连通
    public void union(int p, int q) {
        int rootP = find(p);
        int rootQ = find(q);
        if (rootP == rootQ)
            return;
        parent[rootQ] = rootP;
        // 两个连通分量合并成⼀个连通分量
        count--;
    }
    
    // 判断节点 p 和节点 q 是否连通
    public boolean connected(int p, int q) {
        int rootP = find(p);
        int rootQ = find(q);
        return rootP == rootQ;
    }
    
    public int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]);
        }
        return parent[x];
    }
        
    // 返回图中的连通分量个数
    public int count() {
        return count;
    }
}
```
