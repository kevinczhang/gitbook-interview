# Possible Bipartition



We want to split a group of `n` people (labeled from `1` to `n`) into two groups of **any size**. Each person may dislike some other people, and they should not go into the same group.

Given the integer `n` and the array `dislikes` where `dislikes[i] = [ai, bi]` indicates that the person labeled `ai` does not like the person labeled `bi`, return `true` _if it is possible to split everyone into two groups in this way_.

&#x20;

**Example 1:**

<pre><code>Input: n = 4, dislikes = [[1,2],[1,3],[2,4]]
<strong>Output:
</strong> true
<strong>Explanation:
</strong> group1 [1,4] and group2 [2,3].
</code></pre>

**Example 2:**

<pre><code>Input: n = 3, dislikes = [[1,2],[1,3],[2,3]]
<strong>Output:
</strong> false
</code></pre>

**Example 3:**

<pre><code>Input: n = 5, dislikes = [[1,2],[2,3],[3,4],[4,5],[1,5]]
<strong>Output:
</strong> false
</code></pre>

&#x20;

**Constraints:**

* `1 <= n <= 2000`
* `0 <= dislikes.length <= 104`
* `dislikes[i].length == 2`
* `1 <= dislikes[i][j] <= n`
* `ai < bi`
* All the pairs of `dislikes` are **unique**.

```java
class Solution {
    private boolean ok = true;
    private boolean[] color;
    private boolean[] visited;
    public boolean possibleBipartition(int n, int[][] dislikes) {
        // 图节点编号从 1 开始
        color = new boolean[n + 1];
        visited = new boolean[n + 1];
        // 转化成邻接表表示图结构
        List<Integer>[] graph = buildGraph(n, dislikes);
        for (int v = 1; v <= n; v++) {
            if (!visited[v]) {
                traverse(graph, v);
            }
        }
        return ok;
    }
    
    // 建图函数
    private List<Integer>[] buildGraph(int n, int[][] dislikes) {
        // 图节点编号为 1...n
        List<Integer>[] graph = new LinkedList[n + 1];
        for (int i = 1; i <= n; i++) {
            graph[i] = new LinkedList<>();
        }
        for (int[] edge : dislikes) {
            int v = edge[1];
            int w = edge[0];
            // 「⽆向图」相当于「双向图」
            // v -> w
            graph[v].add(w);
            // w -> v
            graph[w].add(v);
        }
        return graph;
    }
    
    // 和之前的 traverse 函数完全相同
    private void traverse(List<Integer>[] graph, int v) {
        if (!ok) return;
        visited[v] = true;
        for (int w : graph[v]) {
            if (!visited[w]) {
                color[w] = !color[v];
                traverse(graph, w);
            } else {
                if (color[w] == color[v]) {
                    ok = false;
                }
            }
        }
    }
}
```
