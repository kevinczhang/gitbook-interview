# Dijkstra

Template

<pre class="language-java"><code class="lang-java">class State {
<strong>    // 图节点的 id
</strong>    int id;
    // 从 start 节点到当前节点的距离
    int distFromStart;
    State(int id, int distFromStart) {
        this.id = id;
        this.distFromStart = distFromStart;
    }
}

class Solution {
<strong>    // 返回节点 from 到节点 to 之间的边的权重
</strong>    int weight(int from, int to);
    // 输⼊节点 s 返回 s 的相邻节点
    List&#x3C;Integer> adj(int s);
    // 输⼊⼀幅图和⼀个起点 start，计算 start 到其他节点的最短距离
    int[] dijkstra(int start, List&#x3C;Integer>[] graph) {
        // 图中节点的个数
        int V = graph.length;
        // 记录最短路径的权重，你可以理解为 dp table
        // 定义：distTo[i] 的值就是节点 start 到达节点 i 的最短路径权重
        int[] distTo = new int[V];
        // 求最⼩值，所以 dp table 初始化为正⽆穷
        Arrays.fill(distTo, Integer.MAX_VALUE);
        // base case，start 到 start 的最短距离就是 0
        distTo[start] = 0;
        // 优先级队列，distFromStart 较⼩的排在前⾯
        Queue&#x3C;State> pq = new PriorityQueue&#x3C;>((a, b) -> {
            return a.distFromStart - b.distFromStart;
        });
        // 从起点 start 开始进⾏ BFS
        pq.offer(new State(start, 0));
        while (!pq.isEmpty()) {
            State curState = pq.poll();
            int curNodeID = curState.id;
            int curDistFromStart = curState.distFromStart;
            if (curDistFromStart > distTo[curNodeID]) {
                // 已经有⼀条更短的路径到达 curNode 节点了
                continue;
            }
            // 将 curNode 的相邻节点装⼊队列
            for (int nextNodeID : adj(curNodeID)) {
                // 看看从 curNode 达到 nextNode 的距离是否会更短
                int distToNextNode = distTo[curNodeID] + weight(curNodeID, nextNodeID);
                if (distTo[nextNodeID] > distToNextNode) {
                    // 更新 dp table
                    distTo[nextNodeID] = distToNextNode;
                    // 将这个节点以及距离放⼊队列
                    pq.offer(new State(nextNodeID, distToNextNode));
                }
            }
        }
        return distTo;
    }
}
</code></pre>
