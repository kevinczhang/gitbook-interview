# Graph traversal

## 图的遍历

如果图包含环，遍历框架就要⼀个 visited 数组进⾏辅助：

<pre class="language-java" data-title="DFS traversal"><code class="lang-java">// 记录被遍历过的节点
boolean[] visited;
// 记录从起点到当前节点的路径
boolean[] onPath;
/* 图遍历框架 */
void traverse(Graph graph, int s) {
    if (visited[s]) return;
<strong>    // 经过节点 s，标记为已遍历
</strong><strong>    visited[s] = true;
</strong>    // 做选择：标记节点 s 在路径上
    onPath[s] = true;
    for (int neighbor : graph.neighbors(s)) {
        traverse(graph, neighbor);
    }
    // 撤销选择：节点 s 离开路径
    onPath[s] = false;
}
</code></pre>

## Breadth-first Search

{% code title="BFS traversal" %}
```java
// 计算从起点 start 到终点 target 的最近距离
int BFS(Node start, Node target) {
    Queue<Node> q; // 核⼼数据结构
    Set<Node> visited; // 避免⾛回头路
    q.offer(start); // 将起点加⼊队列
    visited.add(start);
    int step = 0; // 记录扩散的步数
    while (q not empty) {
        int sz = q.size();
        /* 将当前队列中的所有节点向四周扩散 */
        for (int i = 0; i < sz; i++) {
            Node cur = q.poll();
            /* 划重点：这⾥判断是否到达终点 */
            if (cur is target)
                return step;
            /* 将 cur 的相邻节点加⼊队列 */
            for (Node x : cur.adj())
                if (x not in visited) {
                    q.offer(x);
                    visited.add(x);
                }
        }
        /* 划重点：更新步数在这⾥ */
        step++;
    }
}
```
{% endcode %}

### Applications of Breadth First Traversal

[https://www.geeksforgeeks.org/applications-of-breadth-first-traversal/](https://www.geeksforgeeks.org/applications-of-breadth-first-traversal/)

**1) Shortest Path and Minimum Spanning Tree for unweighted graph**

In an unweighted graph, the shortest path is the path with least number of edges.

**2) Peer to Peer Networks.**

In Peer to Peer Networks like [BitTorrent](https://www.geeksforgeeks.org/how-bittorrent-works/), Breadth First Search is used to find all neighbor nodes.

**3) Crawlers in Search Engines:**

Crawlers build index using Breadth First. The idea is to start from source page and follow all links from source and keep doing same. Depth First Traversal can also be used for crawlers, but the advantage with Breadth First Traversal is, depth or levels of the built tree can be limited.

**4) Social Networking Websites:**

In social networks, we can find people within a given distance ‘k’ from a person using Breadth First Search till ‘k’ levels.

**5) GPS Navigation systems:**

Breadth First Search is used to find all neighboring locations.

**6) Broadcasting in Network:**

In networks, a broadcasted packet follows Breadth First Search to reach all nodes.

**7) In Garbage Collection:**

Breadth First Search is used in copying garbage collection using [Cheney’s algorithm](http://en.wikipedia.org/wiki/Cheney's\_algorithm). Refer [this](https://lambda.uta.edu/cse5317/notes/node48.html) and for details. Breadth First Search is preferred over Depth First Search because of better locality of reference:

**8)** [**Cycle detection in undirected graph:**](https://www.geeksforgeeks.org/detect-cycle-undirected-graph/)

In undirected graphs, either Breadth First Search or Depth First Search can be used to detect cycle. In directed graph, only depth first search can be used.

**9)**[**Ford–Fulkerson algorithm**](https://www.geeksforgeeks.org/ford-fulkerson-algorithm-for-maximum-flow-problem/):

In Ford-Fulkerson algorithm, we can either use Breadth First or Depth First Traversal to find the maximum flow. Breadth First Traversal is preferred as it reduces worst case time complexity to O(VE2).

**10)**[**To test if a graph is Bipartite**](https://www.geeksforgeeks.org/bipartite-graph/)

We can either use Breadth First or Depth First Traversal.

**11) Path Finding**

We can either use Breadth First or Depth First Traversal to find if there is a path between two vertices.

**12) Finding all nodes within one connected component:**

We can either use Breadth First or Depth First Traversal to find all nodes reachable from a given node.

Many algorithms like [Prim’s Minimum Spanning Tree](https://www.geeksforgeeks.org/greedy-algorithms-set-5-prims-minimum-spanning-tree-mst-2/) and [Dijkstra’s Single Source Shortest Path](https://www.geeksforgeeks.org/greedy-algorithms-set-6-dijkstras-shortest-path-algorithm/) use structure similar to Breadth First Search.

## Depth-first Search

**DFS - Iterative using stack**

**DFS - Recursive**

`以下DFS总结的内容来源：http://chen-tao.github.io/2017/01/26/about-dfs/`

**深度优先搜索(Depth First Search)**

> 假设初始状态是图中所有顶点均未被访问，则从某个顶点v出发，首先访问该顶点，然后依次从它的各个未被访问的邻接点出发深度优先搜索遍历图，直至图中所有和v有路径相通的顶点都被访问到。 若此时尚有其他顶点未被访问到，则另选一个未被访问的顶点作起始点，重复上述过程，直至图中所有顶点都被访问到为止。

### DFS Implementation

#### Graph Node

```java
public calss GraphNode{
  int val;
  List<GraphNode> neighnors;
}
```

为了防止重复，使用一个HashSet来保存已经遍历过的节点（或者使用1维或2维数组，例如节点是数字类型，或者图本身是2维矩阵）

```java
HashSet<GraphNode> visited = new HashSet<GraphNode>();

// boolean[][] visited = new boolean[m][n]
```

#### Recursive DFS

每到一个节点，标记已经被访问过，对邻居里没有访问的节点进行DFS

```java
public void DFS(GraphNode nd){
  //print nd.val
  visited.add(nd);
  for(GraphNode next : nd.neighbours){
    if(!visited.contains(next)){
      DFS(next);
    }
  }
}
```

#### Non-Recursive DFS

非递归版本，相比递归版本效率高，且不会导致栈溢出

```java
public void DFS(GraphNode start){
  Stack<GraphNode> s = new Stack<GraphNode>();
  s.push(start);
  visited.add(start);
  while(!s.empty()){
    GraphNode cur = s.pop();
    //print cur.val
    for(GraphNode next : cur.children){
      if(!visited.contains(next)){
        s.push(next);
        visited.add(next);//mark node as visited when adding to stack.
      }
    }
  }//while end
}
```

#### DFS with depth (for Tree)

深度depth在搜索中记录，递归版本加一个depth参数++就可以了，非递归版本用一个和s平行的栈记录深度

#### DFS for binary tree–PreOrder traversal

DFS对于二叉树而言，其遍历序列就是其前序遍历 Pre-order Traversal。

```java
[preorder(node)] = node.val + [preorder(node.left)] + [preorder(node.right)]
```

### DFS 解题框架模板

修改自：[http://chen-tao.github.io/2017/01/26/about-dfs/](http://chen-tao.github.io/2017/01/26/about-dfs/)

```java
//结果集
public static T ans;
//中间结果集
public static T path;
//问题
public static T problem(){
  ans = new T();
  path = new T();

  dfs(idx ,...); //DFS部分，常用idx作为结果递归的标志
  return ans;
}
//DFS
public static void dfs(int idx, ...){
  if(xxx){//边界条件，递归出口条件
    //用当前path内容生成一部分结果集
    //handle path 
    ans.add(tmp);
    return;
  }
  //递归处理
  path[idx] = true;//递归前假设
  dfs(++idx, ...);//根据不同情况进行处理
  path[idx] = false;//递归后还原
}
```

### Cycle Detection

对DFS稍作修改，可以判断一个有向图是否有回路

在递归版本里，我们队每一个点改为三种标记：

* 未访问过(0)
* 正在访问其邻居节点(1)
* 已经访问完毕该节点以及所有该节点可以到达的节点(2)

什么时候会出现回路？**就是当前节点v的一个邻居u的状态为1的时候。**

因为该节点状态为1，即还没有把它以后的节点全部遍历，所以当前节点v肯定可以从u到达，而现在又可以从v到达u，所以回路构成。
