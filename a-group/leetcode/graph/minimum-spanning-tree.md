# Minimum Spanning Tree



You might wonder: what is a spanning tree? A **spanning tree** is a connected subgraph in an undirected graph where **all vertices** are connected with the **minimum number** of edges. In Figure 9, all pink edges `[(A, B), (A, C), (A, D), (A, E)]` form a tree, which is a spanning tree of this undirected graph. Note that `[(A, E), (A, B), (B, C), (C, D)]` is also a spanning tree of the undirected graph. Thus, an “undirected graph” can have multiple spanning trees.

![](https://leetcode.com/explore/learn/card/Figures/Graph\_Explore/Spanning\_Tree.png)

Figure 9. Spanning tree

After learning what a spanning tree is, you might have another question: what is a **minimum spanning tree**? A minimum spanning tree is a spanning tree with the minimum possible total edge weight in a “weighted undirected graph”. In Figure 10, a spanning tree formed by green edges `[(A, E), (A, B), (B, C), (C, D)]` is one of the minimum spanning trees in this weighted undirected graph. Actually, `[(A, E), (E, D), (A, B), (B, C)]` forms another minimum spanning tree of the weighted undirected graph. Thus, a “weighted undirected graph” can have multiple minimum spanning trees.

![](https://leetcode.com/explore/learn/card/Figures/Graph\_Explore/Minimum\_Spanning\_Tree.png)

Figure 10. Minimum spanning tree

In this chapter, we will learn about the “cut property and two algorithms for constructing a “minimum spanning tree”:

* Kruskal’s Algorithm
* Prim’s algorithm
