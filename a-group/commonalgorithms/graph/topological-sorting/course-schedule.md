# Course Schedule



There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

* For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

&#x20;

**Example 1:**

<pre><code>Input: numCourses = 2, prerequisites = [[1,0]]
<strong>Output:
</strong> true
<strong>Explanation:
</strong> There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
</code></pre>

**Example 2:**

<pre><code>Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
<strong>Output:
</strong> false
<strong>Explanation:
</strong> There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
</code></pre>

&#x20;

**Constraints:**

* `1 <= numCourses <= 2000`
* `0 <= prerequisites.length <= 5000`
* `prerequisites[i].length == 2`
* `0 <= ai, bi < numCourses`
* All the pairs prerequisites\[i] are **unique**.

{% code title="DFS approach" %}
```java
class Solution {
    // 记录⼀次递归堆栈中的节点
    boolean[] onPath;
    // 记录遍历过的节点，防⽌⾛回头路
    boolean[] visited;
    // 记录图中是否有环
    boolean hasCycle = false;
    
    boolean canFinish(int numCourses, int[][] prerequisites) {
        List<Integer>[] graph = buildGraph(numCourses, prerequisites);
        visited = new boolean[numCourses];
        onPath = new boolean[numCourses];
        for (int i = 0; i < numCourses; i++) {
            // 遍历图中的所有节点
            traverse(graph, i);
        }
        // 只要没有循环依赖可以完成所有课程
        return !hasCycle;
    }
    
    void traverse(List<Integer>[] graph, int s) {
        if (onPath[s]) {
            // 出现环
            hasCycle = true;
        }
        if (visited[s] || hasCycle) {
            // 如果已经找到了环，也不⽤再遍历了
            return;
        }
        // 前序代码位置
        visited[s] = true;
        onPath[s] = true;
        for (int t : graph[s]) {
            traverse(graph, t);
        }
        // 后序代码位置
        onPath[s] = false;
    }
    
    List<Integer>[] buildGraph(int numCourses, int[][] prerequisites) {
        // 图中共有 numCourses 个节点
        List<Integer>[] graph = new LinkedList[numCourses];
        for (int i = 0; i < numCourses; i++) {
            graph[i] = new LinkedList<>();
        }
        for (int[] edge : prerequisites) {
            int from = edge[1], to = edge[0];
            // 添加⼀条从 from 指向 to 的有向边
            // 边的⽅向是「被依赖」关系，即修完课程 from 才能修课程 to
            graph[from].add(to);
        }
        return graph;
    }
}
```
{% endcode %}

{% code title="BFS Approach" %}
```java
class Solution {
    // 主函数
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        // 建图，有向边代表「被依赖」关系
        List<Integer>[] graph = buildGraph(numCourses, prerequisites);
        // 构建⼊度数组
        int[] indegree = new int[numCourses];
        for (int[] edge : prerequisites) {
            int from = edge[1], to = edge[0];
            // 节点 to 的⼊度加⼀
            indegree[to]++;
        }
        // 根据⼊度初始化队列中的节点
        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < numCourses; i++) {
            if (indegree[i] == 0) {
                // 节点 i 没有⼊度，即没有依赖的节点
                // 可以作为拓扑排序的起点，加⼊队列
                q.offer(i);
            }
        }
        // 记录遍历的节点个数
        int count = 0;
        // 开始执⾏ BFS 循环
        while (!q.isEmpty()) {
            // 弹出节点 cur，并将它指向的节点的⼊度减⼀
            int cur = q.poll();
            count++;
            for (int next : graph[cur]) {
                indegree[next]--;
                if (indegree[next] == 0) {
                    // 如果⼊度变为 0，说明 next 依赖的节点都已被遍历
                    q.offer(next);
                }
            }
        }
        // 如果所有节点都被遍历过，说明不成环
        return count == numCourses;
    }
    
    List<Integer>[] buildGraph(int numCourses, int[][] prerequisites) {
        // 图中共有 numCourses 个节点
        List<Integer>[] graph = new LinkedList[numCourses];
        for (int i = 0; i < numCourses; i++) {
            graph[i] = new LinkedList<>();
        }
        for (int[] edge : prerequisites) {
            int from = edge[1], to = edge[0];
            // 添加⼀条从 from 指向 to 的有向边
            // 边的⽅向是「被依赖」关系，即修完课程 from 才能修课程 to
            graph[from].add(to);
        }
        return graph;
    }
}
```
{% endcode %}

Code from template

```java

class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (numCourses <= 1)
            return true;
        // Initial graph and indegrees
        Map<Integer, Integer> inDegrees = new HashMap<>();
        Map<Integer, List<Integer>> topoGraph = new HashMap<>();
        for (int i = 0; i < numCourses; i++){
            inDegrees.put(i, 0);
            topoGraph.put(i, new ArrayList<>());
        }

        // Build dependency graph
        for (int[] prereq : prerequisites) {
            int courseTo = prereq[0];
            int courseReq = prereq[1];

            inDegrees.put(courseTo, inDegrees.getOrDefault(courseTo, 0) + 1);
            topoGraph.get(courseReq).add(courseTo);
        }

        // Topological sort
        while (!inDegrees.isEmpty()){
            boolean foundNodeWithZeroInDegree = false;
            for (Integer c : inDegrees.keySet()) {
                if (inDegrees.get(c) != 0) {
                    continue;
                }
                foundNodeWithZeroInDegree = true; 
                for (Integer p : topoGraph.get(c)) {
                    inDegrees.put(p, inDegrees.get(p) - 1);
                }
                inDegrees.remove(c);
                break;
            }
            if (!foundNodeWithZeroInDegree)
                return false;
        }
        return true;
    }
}

```
