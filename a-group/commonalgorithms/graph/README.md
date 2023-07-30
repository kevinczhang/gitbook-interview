---
description: Common algorithms for graph
coverY: 0
---

# Graph

## Graph representation

```java
// 邻接表
// graph[x] 存储 x 的所有邻居节点
List<Integer>[] graph;
// 邻接矩阵
// matrix[x][y] 记录 x 是否有⼀条指向 y 的边
boolean[][] matrix;
```

有向加权图怎么实现

```java
// 邻接表
// graph[x] 存储 x 的所有邻居节点以及对应的权重
List<int[]>[] graph;
// 邻接矩阵
// matrix[x][y] 记录 x 指向 y 的边的权重，0 表示不相邻
int[][] matrix;
```

## Shortest Path and Dijkstra's Algorithm

StackOverflow: [What is difference between BFS and Dijkstra's algorithms when looking for shortest path?](https://stackoverflow.com/questions/25449781/what-is-difference-between-bfs-and-dijkstras-algorithms-when-looking-for-shorte)

> Breadth-first search is just Dijkstra's algorithm with all edge weights equal to 1.
>
> Dijkstra's algorithm is conceptually breadth-first search that respects edge costs.
>
> The process for exploring the graph is structurally the same in both cases.

[Aos Dabbagh: Understanding Dijkstra's Algorithm](https://aos.github.io/2018/02/24/understanding-dijkstras-algorithm/)

> One of **Dijkstra’s** **algorithm** modifications on **breadth-first search** is its use of a **priority** **queue** instead of a normal queue. With a priority queue, each task added to the queue has a “**priority**” and will slot in accordingly into the queue based on its priority level.

[UIUC CS473: Breadth First Search, Dijkstra’s Algorithm for Shortest Paths](https://courses.engr.illinois.edu/cs473/sp2011/Lectures/03\_class.pdf) (PDF)

无权图可以用BFS，到达目标点遍历的层数就是最短路径。

有权图则需要用Dijkstra's Algorithm。

## Reference

* [Stanford CS97si](https://web.stanford.edu/class/cs97si/06-basic-graph-algorithms.pdf)
* [BFS](http://www.mathcs.emory.edu/\~cheung/Courses/323/Syllabus/Graph/bfs.html)

Dijkstra's Algorithm

* [UIUC CS473: Breadth First Search, Dijkstra’s Algorithm for Shortest Paths](https://courses.engr.illinois.edu/cs473/sp2011/Lectures/03\_class.pdf) (PDF)
* [What is difference between BFS and Dijkstra's algorithms when looking for shortest path?](https://stackoverflow.com/questions/25449781/what-is-difference-between-bfs-and-dijkstras-algorithms-when-looking-for-shorte)
* [Aos Dabbagh: Understanding Dijkstra's Algorith](broken-reference)
