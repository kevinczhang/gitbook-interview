# Is Graph Bipartite?



There is an **undirected** graph with `n` nodes, where each node is numbered between `0` and `n - 1`. You are given a 2D array `graph`, where `graph[u]` is an array of nodes that node `u` is adjacent to. More formally, for each `v` in `graph[u]`, there is an undirected edge between node `u` and node `v`. The graph has the following properties:

* There are no self-edges (`graph[u]` does not contain `u`).
* There are no parallel edges (`graph[u]` does not contain duplicate values).
* If `v` is in `graph[u]`, then `u` is in `graph[v]` (the graph is undirected).
* The graph may not be connected, meaning there may be two nodes `u` and `v` such that there is no path between them.

A graph is **bipartite** if the nodes can be partitioned into two independent sets `A` and `B` such that **every** edge in the graph connects a node in set `A` and a node in set `B`.

Return `true` _if and only if it is **bipartite**_.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/21/bi2.jpg)

<pre><code>Input: graph = [[1,2,3],[0,2],[0,1,3],[0,2]]
<strong>Output:
</strong> false
<strong>Explanation:
</strong> There is no way to partition the nodes into two independent sets such that every edge connects a node in one and a node in the other.
</code></pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/21/bi1.jpg)

<pre><code>Input: graph = [[1,3],[0,2],[1,3],[0,2]]
<strong>Output:
</strong> true
<strong>Explanation:
</strong> We can partition the nodes into two sets: {0, 2} and {1, 3}.
</code></pre>

&#x20;

**Constraints:**

* `graph.length == n`
* `1 <= n <= 100`
* `0 <= graph[u].length < n`
* `0 <= graph[u][i] <= n - 1`
* `graph[u]` does not contain `u`.
* All the values of `graph[u]` are **unique**.
* If `graph[u]` contains `v`, then `graph[v]` contains `u`.

{% code title="DFS Approach" %}
```java
class Solution {
    // 记录图是否符合⼆分图性质
    private boolean ok = true;
    // 记录图中节点的颜⾊，false 和 true 代表两种不同颜⾊
    private boolean[] color;
    // 记录图中节点是否被访问过
    private boolean[] visited;
    
    // 主函数，输⼊邻接表，判断是否是⼆分图
    public boolean isBipartite(int[][] graph) {
        int n = graph.length;
        color = new boolean[n];
        visited = new boolean[n];
        // 因为图不⼀定是联通的，可能存在多个⼦图
        // 所以要把每个节点都作为起点进⾏⼀次遍历
        // 如果发现任何⼀个⼦图不是⼆分图，整幅图都不算⼆分图
        for (int v = 0; v < n; v++) {
            if (!visited[v]) {
                traverse(graph, v);
            }
        }
        return ok;
    }
    
    // DFS 遍历框架
    private void traverse(int[][] graph, int v) {
        // 如果已经确定不是⼆分图了，就不⽤浪费时间再递归遍历了
        if (!ok) return;
        visited[v] = true;
        for (int w : graph[v]) {
            if (!visited[w]) {
                // 相邻节点 w 没有被访问过
                // 那么应该给节点 w 涂上和节点 v 不同的颜⾊
                color[w] = !color[v];
                // 继续遍历 w
                traverse(graph, w);
            } else {
                // 相邻节点 w 已经被访问过
                // 根据 v 和 w 的颜⾊判断是否是⼆分图
                if (color[w] == color[v]) {
                    // 若相同，则此图不是⼆分图
                    ok = false;
                }
            }
        }
    }
}
```
{% endcode %}

{% code title="BFS Approach" %}
```java
class Solution {
    // 记录图是否符合⼆分图性质
    private boolean ok = true;
    // 记录图中节点的颜⾊，false 和 true 代表两种不同颜⾊
    private boolean[] color;
    // 记录图中节点是否被访问过
    private boolean[] visited;
    
    public boolean isBipartite(int[][] graph) {
        int n = graph.length;
        color = new boolean[n];
        visited = new boolean[n];
        for (int v = 0; v < n; v++) {
            if (!visited[v]) {
                // 改为使⽤ BFS 函数
                bfs(graph, v);
            }
        }
        return ok;
    }
    
    // 从 start 节点开始进⾏ BFS 遍历
    private void bfs(int[][] graph, int start) {
        Queue<Integer> q = new LinkedList<>();
        visited[start] = true;
        q.offer(start);
        while (!q.isEmpty() && ok) {
            int v = q.poll();
            // 从节点 v 向所有相邻节点扩散
            for (int w : graph[v]) {
                if (!visited[w]) {
                    // 相邻节点 w 没有被访问过
                    // 那么应该给节点 w 涂上和节点 v 不同的颜⾊
                    color[w] = !color[v];
                    // 标记 w 节点，并放⼊队列
                    visited[w] = true;
                    q.offer(w);
                } else {
                    // 相邻节点 w 已经被访问过
                    // 根据 v 和 w 的颜⾊判断是否是⼆分图
                    if (color[w] == color[v]) {
                        // 若相同，则此图不是⼆分图
                        ok = false;
                    }
                }
            }
        }
    }
}
```
{% endcode %}
