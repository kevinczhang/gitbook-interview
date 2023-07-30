# Breadth-First Search



Previously, we discussed the “depth-first search” algorithm. This section will talk about a closely related and equally popular algorithm called “breadth-first search”. Similarly, the “breadth-first search” algorithm can traverse all vertices of a “graph” and traverse all paths between two vertices. However, the most advantageous use case of “breadth-first search” is to efficiently find the shortest path between two vertices in a “graph” where **all edges have equal and positive weights**.

Although the “depth-first search” algorithm can find the shortest path between two vertices in a “graph” with equal and positive weights, it must traverse all paths between two vertices before finding the shortest one. The “breadth-first search” algorithm, in most cases, can find the shortest path without traversing all paths. This is because when using "breadth-first search", as soon as a path between the source vertex and target vertex is found, it is guaranteed to be the shortest path between the two nodes.

In Figure 8, the vertices are `[A, C, D, B, E]`. Given vertices `A` and `B`, there are two paths between them. One path is `[A, C, D, B]`, and the other is `[A, E, B]`. Obviously, `[A, E, B]` is the shortest path between `A` and `B`.

![](https://leetcode.com/explore/learn/card/Figures/Graph\_Explore/An\_Undirected\_Graph.png)

Figure 8. An undirected graph

In Graph theory, the primary use cases of the “breadth-first search” (“BFS”) algorithm are:

1. Traversing all vertices in the “graph”;
2. Finding the shortest path between two vertices in a graph where **all edges have equal and positive weights**.
