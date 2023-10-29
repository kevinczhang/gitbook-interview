# Network Delay Time



You are given a network of `n` nodes, labeled from `1` to `n`. You are also given `times`, a list of travel times as directed edges `times[i] = (ui, vi, wi)`, where `ui` is the source node, `vi` is the target node, and `wi` is the time it takes for a signal to travel from source to target.

We will send a signal from a given node `k`. Return _the **minimum** time it takes for all the_ `n` _nodes to receive the signal_. If it is impossible for all the `n` nodes to receive the signal, return `-1`.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/05/23/931\_example\_1.png)

<pre><code>Input: times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2
<strong>Output:
</strong> 2
</code></pre>

**Example 2:**

<pre><code>Input: times = [[1,2,1]], n = 2, k = 1
<strong>Output:
</strong> 1
</code></pre>

**Example 3:**

<pre><code>Input: times = [[1,2,1]], n = 2, k = 2
<strong>Output:
</strong> -1
</code></pre>

&#x20;

**Constraints:**

* `1 <= k <= n <= 100`
* `1 <= times.length <= 6000`
* `times[i].length == 3`
* `1 <= ui, vi <= n`
* `ui != vi`
* `0 <= wi <= 100`
* All the pairs `(ui, vi)` are **unique**. (i.e., no multiple edges.)

```java
class Solution {    
    public int networkDelayTime(int[][] times, int n, int k) {
        // 节点编号是从 1 开始的，所以要⼀个⼤⼩为 n + 1 的邻接表
        List<int[]>[] graph = new LinkedList[n + 1];
        for (int i = 1; i <= n; i++) {
            graph[i] = new LinkedList<>();
        }
        // 构造图
        for (int[] edge : times) {
            int from = edge[0];
            int to = edge[1];
            int weight = edge[2];
            // from -> List<(to, weight)>
            // 邻接表存储图结构，同时存储权重信息
            graph[from].add(new int[]{to, weight});
        }
        // 启动 dijkstra 算法计算以节点 k 为起点到其他节点的最短路径
        int[] distTo = dijkstra(k, graph);
        // 找到最⻓的那⼀条最短路径
        int res = 0;
        for (int i = 1; i < distTo.length; i++) {
            if (distTo[i] == Integer.MAX_VALUE) {
                // 有节点不可达，返回 -1
                return -1;
            }
            res = Math.max(res, distTo[i]);
        }
        return res;
    }
    
    class State {
        // 图节点的 id
        int id;
        // 从 start 节点到当前节点的距离
        int distFromStart;
        State(int id, int distFromStart) {
            this.id = id;
            this.distFromStart = distFromStart;
        }
    }
    
    // 输⼊⼀个起点 start，计算从 start 到其他节点的最短距离
    int[] dijkstra(int start, List<int[]>[] graph) {
        // 定义：distTo[i] 的值就是起点 start 到达节点 i 的最短路径权重
        int[] distTo = new int[graph.length];
        Arrays.fill(distTo, Integer.MAX_VALUE);
        // base case，start 到 start 的最短距离就是 0
        distTo[start] = 0;
        // 优先级队列，distFromStart 较⼩的排在前⾯
        Queue<State> pq = new PriorityQueue<>((a, b) -> {
            return a.distFromStart - b.distFromStart;
        });
        // 从起点 start 开始进⾏ BFS
        pq.offer(new State(start, 0));
        while (!pq.isEmpty()) {
            State curState = pq.poll();
            int curNodeID = curState.id;
            int curDistFromStart = curState.distFromStart;
            if (curDistFromStart > distTo[curNodeID]) {
                continue;
            }
            // 将 curNode 的相邻节点装⼊队列
            for (int[] neighbor : graph[curNodeID]) {
                int nextNodeID = neighbor[0];
                int distToNextNode = distTo[curNodeID] + neighbor[1];
                // 更新 dp table
                if (distTo[nextNodeID] > distToNextNode) {
                    distTo[nextNodeID] = distToNextNode;
                    pq.offer(new State(nextNodeID, distToNextNode));
                }
            }
        }
        return distTo;
    }
}
```

Code from template

```java
/*
Step 1: Create a Map of start and end nodes with weight
        1 -> {2,1},{3,2}
        2 -> {4,4},{5,5}
        3 -> {5,3}
        4 ->
        5 ->

Step 2: create a result array where we will keep track the minimum distance to rech end of the node from start node

Step 3: Create a Queue and add starting position with it's weight and add it's reachable distance with increament of own't weight plus a weight require to reach at the end node from start node.
        We keep adding and removing pairs from queue and updating result array as well.

Step 4: find the maximum value from result array:

*/

class Solution {
    public int networkDelayTime(int[][] times, int n, int k) {
        
        //Step 1
        Map<Integer, Map<Integer, Integer>> map = new HashMap<>();
        
        for(int[] time : times) {
            int start = time[0];
            int end = time[1];
            int weight = time[2];
            
            map.putIfAbsent(start, new HashMap<>());
            map.get(start).put(end, weight);
        }
        
         // Step 2
        int[] dis = new int[n+1];
        Arrays.fill(dis, Integer.MAX_VALUE);
        dis[k] = 0;
        
        Queue<int[]> queue = new LinkedList<>();
        queue.add(new int[]{k,0});
        
        //Step 3:
        while(!queue.isEmpty()) {
            int[] cur = queue.poll();
            int curNode = cur[0];
            int curWeight = cur[1];
            
            for(int next : map.getOrDefault(curNode, new HashMap<>()).keySet()) {
                int nextweight = map.get(curNode).get(next);
                
                if(curWeight + nextweight < dis[next]) {
                    dis[next] = curWeight + nextweight;
                    queue.add(new int[]{next, curWeight + nextweight});
                }
            }
        }
        
        //Step 4:
        int res = 0;
        for(int i=1; i<=n; i++) {
            if(dis[i] > res) {
                res = Math.max(res, dis[i]);
            } 
        }
        
        return res == Integer.MAX_VALUE ? -1 : res;
    }
}
```
