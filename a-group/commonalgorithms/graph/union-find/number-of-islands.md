---
description: Typical Breadth first search
---

# Number of Islands

Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

```
Input:
11110
11010
11000
00000

Output: 1
```

**Example 2:**

```
Input:
11000
11000
00100
00011

Output: 3
```

```java
class Solution {
    
    private int[][] directions = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
    private UF uf;
    private int rows, cols, countIslands;
    
    public int numIslands(char[][] grid) {
        if (grid.length == 0) return 0;
        
        rows = grid.length;
        cols = grid[0].length;
        uf = new UF(rows * cols);
        
        countIslands = 0;
        
        for (int x = 0; x < rows; x++) {
            for (int y = 0; y < cols; y++) {
                // If value 1, union with adjacent
                if (grid[x][y] == '1') {
                    countIslands++;
                    unionAround(x, y, grid);
                }
            }
        }
        
        return countIslands;
    }
    
    private void unionAround(int x, int y, char[][] grid) {
        int mark = x * cols + y;
        for (int[] dir : directions) {
            int nx = x + dir[0];
            int ny = y + dir[1];
            if (nx >= 0 && nx < rows && ny >= 0 && ny < cols && grid[nx][ny] == '1') {
                if (uf.union(nx * cols + ny, mark)) {
                    countIslands--;
                }
            }
        }
    }
    
    class UF {
        int[] parent;

        public UF(int n) {
            parent = new int[n];
            for (int i = 0; i < n; i++) {
                parent[i] = i;
            }
        }

        private int find(int x) {
            if (parent[x] == x) {
                return x;
            }
            return parent[x] = find(parent[x]); // Path compression
        }

        // Return false if x and y are in the same disjoint set already
        public boolean union(int x, int y) {
            int rootX = find(x);
            int rootY = find(y);
            if (rootX == rootY) {
                return false;
            }
            parent[rootX] = rootY;
            return true;
        }
    }
```

```java
class Solution {
    public int numIslands(char[][] grid) {
        int res = 0;
        for (int row = 0; row < grid.length; row++) {
            for (int col = 0; col < grid[0].length; col++) {
                if (grid[row][col] == '0' || grid[row][col] == '*') {
                    continue;
                }
                res++;
                Queue<String> queue = new LinkedList<String>();
                queue.offer(row + "," + col);
                grid[row][col] = '*';
                while(!queue.isEmpty()) {
                    String curCors = queue.poll();
                    String[] cors = curCors.split(",");
                    int rowNum = Integer.valueOf(cors[0]);
                    int colNum = Integer.valueOf(cors[1]);                    
                    
                    if(colNum + 1 < grid[0].length && grid[rowNum][colNum + 1] == '1') {
                        queue.offer(rowNum + "," + String.valueOf(colNum + 1));
                        grid[rowNum][colNum + 1] = '*';
                    }
                    if(rowNum + 1 < grid.length && grid[rowNum + 1][colNum] == '1') {
                        queue.offer(String.valueOf(rowNum + 1) + "," + colNum);
                        grid[rowNum + 1][colNum] = '*';
                    }
                    if(colNum - 1 >= 0 && grid[rowNum][colNum - 1] == '1') {
                        queue.offer(rowNum + "," + String.valueOf(colNum - 1));
                        grid[rowNum][colNum - 1] = '*';
                    }
                    if(rowNum - 1 >= 0 && grid[rowNum - 1][colNum] == '1') {
                        queue.offer(String.valueOf(rowNum - 1) + "," + colNum);
                        grid[rowNum - 1][colNum] = '*';
                    }
                }
            }
        }
        return res;
    }
}
```
