# Path with Maximum Probability



You are given an undirected weighted graph of `n` nodes (0-indexed), represented by an edge list where `edges[i] = [a, b]` is an undirected edge connecting the nodes `a` and `b` with a probability of success of traversing that edge `succProb[i]`.

Given two nodes `start` and `end`, find the path with the maximum probability of success to go from `start` to `end` and return its success probability.

If there is no path from `start` to `end`, **return 0**. Your answer will be accepted if it differs from the correct answer by at most **1e-5**.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/09/20/1558\_ex1.png)

<pre><code>Input: n = 3, edges = [[0,1],[1,2],[0,2]], succProb = [0.5,0.5,0.2], start = 0, end = 2
<strong>Output:
</strong> 0.25000
<strong>Explanation:
</strong> There are two paths from start to end, one having a probability of success = 0.2 and the other has 0.5 * 0.5 = 0.25.
</code></pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/09/20/1558\_ex2.png)

<pre><code>Input: n = 3, edges = [[0,1],[1,2],[0,2]], succProb = [0.5,0.5,0.3], start = 0, end = 2
<strong>Output:
</strong> 0.30000
</code></pre>

**Example 3:**

![](https://assets.leetcode.com/uploads/2019/09/20/1558\_ex3.png)

<pre><code>Input: n = 3, edges = [[0,1]], succProb = [0.5], start = 0, end = 2
<strong>Output:
</strong> 0.00000
<strong>Explanation:
</strong> There is no path between 0 and 2.
</code></pre>

&#x20;

**Constraints:**

* `2 <= n <= 10^4`
* `0 <= start, end < n`
* `start != end`
* `0 <= a, b < n`
* `a != b`
* `0 <= succProb.length == edges.length <= 2*10^4`
* `0 <= succProb[i] <= 1`
* There is at most one edge between every two nodes.

```java
class Solution {
    public double maxProbability(int n, int[][] edges, double[] succProb, int start, int end) {
        List<double[]>[] graph = new LinkedList[n];
        for (int i = 0; i < n; i++) {
            graph[i] = new LinkedList<>();
        }
        // 构造邻接表结构表示图
        for (int i = 0; i < edges.length; i++) {
            int from = edges[i][0];
            int to = edges[i][1];
            double weight = succProb[i];
            // ⽆向图就是双向图；先把 int 统⼀转成 double，待会再转回来
            graph[from].add(new double[]{(double)to, weight});
            graph[to].add(new double[]{(double)from, weight});
        }
        return dijkstra(start, end, graph);
    }
    
    double dijkstra(int start, int end, List<double[]>[] graph) {
        // 定义：probTo[i] 的值就是节点 start 到达节点 i 的最⼤概率
        double[] probTo = new double[graph.length];
        // dp table 初始化为⼀个取不到的最⼩值
        Arrays.fill(probTo, -1);
        // base case，start 到 start 的概率就是 1
        probTo[start] = 1;
        // 优先级队列，probFromStart 较⼤的排在前⾯
        Queue<State> pq = new PriorityQueue<>((a, b) -> {
            return Double.compare(b.probFromStart, a.probFromStart);
        });
                // 从起点 start 开始进⾏ BFS
        pq.offer(new State(start, 1));
        while (!pq.isEmpty()) {
            State curState = pq.poll();
            int curNodeID = curState.id;
            double curProbFromStart = curState.probFromStart;
            // 遇到终点提前返回
            if (curNodeID == end) {
                return curProbFromStart;
            }
            if (curProbFromStart < probTo[curNodeID]) {
                // 已经有⼀条概率更⼤的路径到达 curNode 节点了
                continue;
            }
            // 将 curNode 的相邻节点装⼊队列
            for (double[] neighbor : graph[curNodeID]) {
                int nextNodeID = (int)neighbor[0];
                // 看看从 curNode 达到 nextNode 的概率是否会更⼤
                double probToNextNode = probTo[curNodeID] * neighbor[1];
                if (probTo[nextNodeID] < probToNextNode) {
                    probTo[nextNodeID] = probToNextNode;
                    pq.offer(new State(nextNodeID, probToNextNode));
                }
            }
        }
        // 如果到达这⾥，说明从 start 开始⽆法到达 end，返回 0
        return 0.0;
    }
}

class State {
    // 图节点的 id
    int id;
    // 从 start 节点到达当前节点的概率
    double probFromStart;
    State(int id, double probFromStart) {
        this.id = id;
        this.probFromStart = probFromStart;
    }
}
```

Code with template

```java
class Solution {
    public double maxProbability(int n, int[][] edges, 
        double[] succProb, int start, int end) {
        
        Map<Integer, Map<Integer, Double>> map = new HashMap<>();        
        for(int i=0; i<edges.length; i++){
            map.putIfAbsent(edges[i][0], new HashMap<>());
            map.putIfAbsent(edges[i][1], new HashMap<>());
            map.get(edges[i][0]).put(edges[i][1], succProb[i]);
            map.get(edges[i][1]).put(edges[i][0], succProb[i]);
        }
        
        Set<Integer> visited = new HashSet<>();
        
        PriorityQueue<double[]> queue = 
            new PriorityQueue<double[]>((a, b) -> new Double(b[1]).compareTo(new Double(a[1])));
        queue.add(new double[]{start, 1.0});
        
        while(!queue.isEmpty()) {
            double[] cur = queue.poll();
            
            int curNode = (int)cur[0];
            double curWeight = cur[1];
            
            if(curNode == end) {
                return curWeight;
            }
            
            if(!visited.contains(curNode)) {
                visited.add(curNode);                
                for(Map.Entry<Integer, Double> next: 
                    map.getOrDefault(curNode, new HashMap<>()).entrySet()) {
                    int nKey = next.getKey();
                    double nextWeight = next.getValue();                    
                    queue.add(new double[]{nKey, curWeight * nextWeight});
                }
            }
        }
        return 0;
    }
}
```
