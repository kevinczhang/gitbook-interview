# Spiral Matrix

Given a matrix of\_m\_x\_n\_elements (\_m\_rows,\_n\_columns), return all elements of the matrix in spiral order.

**Example 1:**

```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output: [1,2,3,6,9,8,7,4,5]
```

**Example 2:**

```
Input:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

## Analysis

### Simulation 模拟法

也就是按照人实现的方式，顺时针遍历矩阵即可。

标记已遍历的元素避免重复遍历陷入死循环，两种方法：

1 新建一个二维数组seen\[m]\[n]，seen\[i]\[j]对应matrix\[i]\[j]，遍历过的元素设为true

2 设定上下左右四个边界值，即rowLower, rowUpper, colLower, colUpper, 在转换遍历方向时增减边界值的大小

### Layer-by-Layer <a href="#approach-2-layerbylayer" id="approach-2-layerbylayer"></a>

其实是转化思路，从另一个角度看，spiral遍历时恰好是一层一层元素的顺时针输出:

@LeetCode![](broken-reference)

```java
int r1 = 0, r2 = matrix.length - 1;
int c1 = 0, c2 = matrix[0].length - 1;
while (r1 <= r2 && c1 <= c2) {
...
}
```

## Solution

**Simulation** - Setting Upper Lower Bounds ofRow, Column indexes - (3ms 10.49%)

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> ans = new LinkedList<Integer>();
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return ans;
        }   
        int m = matrix.length;
        int n = matrix[0].length;
        int total = m * n;
        int row = 0, col = 0;

        // lower and upper bound for row, col indexes
        int rowLower = 0, rowUpper = m - 1;
        int colLower = 0, colUpper = n - 1;

        // direction offset for row index (dir[][0]), column index (dir[][1]) 
        int[][] dir = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};

        // mapping of RIGHT, DOWN, LEFT, UP to indexes in dir[][] 
        int RIGHT = 0, DOWN = 1, LEFT = 2, UP = 3;

        // initial direction
        int toward = RIGHT;

        for (int k = 0; k < total; k++) {
            ans.add(matrix[row][col]);

            // change direction, change boundary limits when hitting boundaries
            if (toward == RIGHT && col == colUpper) {
                rowLower++;
                toward = (toward + 1) % 4;
            } else if (toward == DOWN && row == rowUpper) {
                colUpper--;
                toward = (toward + 1) % 4;
            } else if (toward == LEFT && col == colLower) {
                rowUpper--;
                toward = (toward + 1) % 4;
            } else if (toward == UP && row == rowLower) {
                colLower++;
                toward = (toward + 1) % 4;
            } 

            row = row + dir[toward][0];
            col = col + dir[toward][1];
        }
        return ans;
    }
}
```

Simulation - Additional auxiliary matrix `seen[][]` for visited elements

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List ans = new ArrayList();
        if (matrix.length == 0) return ans;
        int R = matrix.length, C = matrix[0].length;
        boolean[][] seen = new boolean[R][C];
        int[] dr = {0, 1, 0, -1};
        int[] dc = {1, 0, -1, 0};
        int r = 0, c = 0, di = 0;
        for (int i = 0; i < R * C; i++) {
            ans.add(matrix[r][c]);
            seen[r][c] = true;
            int cr = r + dr[di];
            int cc = c + dc[di];
            if (0 <= cr && cr < R && 0 <= cc && cc < C && !seen[cr][cc]){
                r = cr;
                c = cc;
            } else {
                di = (di + 1) % 4;
                r += dr[di];
                c += dc[di];
            }
        }
        return ans;
    }
}
```

Layer by Layer

```java
class Solution {
    public List < Integer > spiralOrder(int[][] matrix) {
        List ans = new ArrayList();
        if (matrix.length == 0)
            return ans;
        int r1 = 0, r2 = matrix.length - 1;
        int c1 = 0, c2 = matrix[0].length - 1;
        while (r1 <= r2 && c1 <= c2) {
            for (int c = c1; c <= c2; c++) ans.add(matrix[r1][c]);
            for (int r = r1 + 1; r <= r2; r++) ans.add(matrix[r][c2]);
            if (r1 < r2 && c1 < c2) {
                for (int c = c2 - 1; c > c1; c--) ans.add(matrix[r2][c]);
                for (int r = r2; r > r1; r--) ans.add(matrix[r][c1]);
            }
            r1++;
            r2--;
            c1++;
            c2--;
        }
        return ans;
    }
}
```

## Reference

[https://leetcode.com/articles/spiral-matrix/](https://leetcode.com/articles/spiral-matrix/)
