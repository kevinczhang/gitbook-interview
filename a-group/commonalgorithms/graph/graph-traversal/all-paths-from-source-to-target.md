---
description: Typical DFS
---

# All Paths From Source to Target



Given a directed acyclic graph (**DAG**) of `n` nodes labeled from `0` to `n - 1`, find all possible paths from node `0` to node `n - 1` and return them in **any order**.

The graph is given as follows: `graph[i]` is a list of all nodes you can visit from node `i` (i.e., there is a directed edge from node `i` to node `graph[i][j]`).

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/28/all\_1.jpg)

<pre><code>Input: graph = [[1,2],[3],[3],[]]
<strong>Output:
</strong> [[0,1,3],[0,2,3]]
<strong>Explanation:
</strong> There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.
</code></pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/09/28/all\_2.jpg)

<pre><code>Input: graph = [[4,3,1],[3,2,4],[3],[4],[]]
<strong>Output:
</strong> [[0,4],[0,3,4],[0,1,3,4],[0,1,2,3,4],[0,1,4]]
</code></pre>

&#x20;

**Constraints:**

* `n == graph.length`
* `2 <= n <= 15`
* `0 <= graph[i][j] < n`
* `graph[i][j] != i` (i.e., there will be no self-loops).
* All the elements of `graph[i]` are **unique**.
* The input graph is **guaranteed** to be a **DAG**.

```java
class Solution {
    // 记录所有路径
    List<List<Integer>> res = new LinkedList<>();
    
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        // 维护递归过程中经过的路径
        LinkedList<Integer> path = new LinkedList<>();
        traverse(graph, 0, path);
        return res;
    }
    
    /* 图的遍历框架 */
    void traverse(int[][] graph, int s, LinkedList<Integer> path) {
        // 添加节点 s 到路径
        path.addLast(s);
        int n = graph.length;
        if (s == n - 1) {
            // 到达终点
            res.add(new LinkedList<>(path));
            // 可以在这直接 return，但要 removeLast 正确维护 path
            // path.removeLast();
            // return;
            // 不 return 也可以，因为图中不包含环，不会出现⽆限递归
        }
        // 递归每个相邻节点
        for (int v : graph[s]) {
            traverse(graph, v, path);
        }
        // 从路径移出节点 s
        path.removeLast();
    }
}
```
