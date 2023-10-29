---
description: Common algorithms for graph
coverY: 0
---

# Graph

**SSSP Algorithm**

Problem Used [https://leetcode.com/problems/network-delay-time/](https://leetcode.com/problems/network-delay-time/)

**Time Complexity**\
**Dijkstra** - V + ElogE - SSSP Single Source Shortest Path\
**Bellman Ford** - VE - SSSP\
**Floyd Warshall** - V^3 - MSSP

**Dijkstra**

```java
class Solution {
    public int networkDelayTime(int[][] times, int N, int K) {
        List<int[]>[] adj = new ArrayList[N];
        for (int i = 0; i < N; i++) {
            adj[i] = new ArrayList<>();
        }

        for (int[] t : times) {
            adj[t[0] - 1].add(new int[]{t[1] - 1, t[2]});
        }

        int[] dist = new int[N];
        Arrays.fill(dist, -1);

        dist[K - 1] = 0;
        Queue<int[]> minHeap = new PriorityQueue<>((a, b) -> Integer.compare(a[1], b[1]));
        minHeap.offer(new int[]{K - 1, 0});

        while (minHeap.size() > 0) {
            int curr = minHeap.peek()[0];
            minHeap.poll();
            for (int[] pair : adj[curr]) {
                int next = pair[0];
                int weight = pair[1];
                int d = dist[curr] + weight;
                if (dist[next] == -1 || dist[next] > d) {
                    dist[next] = d;
                    minHeap.offer(new int[]{next, dist[next]});
                }
            }
        }

        int maxwait = 0;
        for (int i = 0; i < N; i++) {
            if(dist[i] == -1) 
                return -1;
            maxwait = Math.max(maxwait, dist[i]);
        }
        return maxwait;
    }
}
```

***

**Bellman Ford**

```java
class Solution {
    public int networkDelayTime(int[][] times, int N, int K) {
        int[] dist = new int[N + 1];
        Arrays.fill(dist, Integer.MAX_VALUE);
        
        dist[K] = 0;
        for(int i = 1; i < N; i++) {
            for(int[] e : times) {
                int u = e[0], v = e[1], w = e[2];
                if(dist[u] != Integer.MAX_VALUE && dist[v] > dist[u] + w)
                    dist[v] = dist[u] + w;
            }
        }
        
        int maxwait = 0;
        for (int i = 1; i <= N; i++)
            maxwait = Math.max(maxwait, dist[i]);
        return maxwait == Integer.MAX_VALUE ? -1 : maxwait;
    }
}
```

**Bellman Short Code**

```java
class Solution {
    public int networkDelayTime(int[][] times, int N, int K) {
        int[] dist = new int[N];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[K - 1] = 0;
        for(int i = 1; i < N; i++)
            for(int[] e : times)
                if(dist[e[0] - 1] != Integer.MAX_VALUE && dist[e[1] - 1] > dist[e[0] - 1] + e[2])
                    dist[e[1] - 1] = dist[e[0] - 1] + e[2];
        
        int maxwait = Arrays.stream(dist).max().getAsInt();
        return maxwait == Integer.MAX_VALUE ? -1 : maxwait;
    }
}
```

***

**Floyd Warshall**

```java
class Solution {
    public int networkDelayTime(int[][] times, int N, int K) {
        int MAX = 1000000;
        int[][] dist = new int[N][N];
        for(int i = 0; i < N; i++)
            Arrays.fill(dist[i], MAX);
        for(int i = 0; i < N; i++)
            dist[i][i] = 0;
        for(int[] e : times)
            dist[e[0] - 1][e[1] - 1] = e[2];
        
        for(int k = 0; k < N; k++)
            for(int i = 0; i < N; i++)
                for(int j = 0; j < N; j++) 
                    dist[i][j] = Math.min(dist[i][j], dist[i][k] + dist[k][j]);
        
        int maxwait = 0;
        for(int i = 0; i < N; i++)
            maxwait = Math.max(maxwait, dist[K - 1][i]);
        return maxwait == MAX ? -1 : maxwait;
    }
}
```

***

**MST Algorithms**

Problem Used - [https://leetcode.com/problems/min-cost-to-connect-all-points/](https://leetcode.com/problems/min-cost-to-connect-all-points/)

**Prims**

// Shorter

```java
class Solution {
    public int minCostConnectPoints(int[][] p) {
        int n = p.length;
        PriorityQueue<int[]> pq = new PriorityQueue<>((u, v) -> Integer.compare(u[2], v[2]));
        pq.offer(new int[] {0, 0, 0});
        boolean[] mst = new boolean[n];
        int selectedEdges = 0;
        int cost = 0;
        while(pq.size() > 0 || selectedEdges < n - 1) {
            int[] e = pq.poll();
            if(mst[e[1]])
                continue;
            mst[e[1]] = true;
            cost += e[2];
            selectedEdges++;
            for(int j = 0; j < n; j++)
                if(!mst[j])
                    pq.offer(new int[] {e[1], j, Math.abs(p[e[1]][0] - p[j][0]) + Math.abs(p[e[1]][1] - p[j][1])});
        }
        
        return cost;
    }
}
```

// Longer

```java
class Solution {
    public int minCostConnectPoints(int[][] p) {
        int n = p.length;
        int[][] dist = new int[n][n];
        
        for(int i = 0; i < n; i++)
            for(int j = 0; j < n; j++)
                dist[i][j] = Math.abs(p[i][0] - p[j][0]) + Math.abs(p[i][1] - p[j][1]);
        
        PriorityQueue<int[]> pq = new PriorityQueue<>((u, v) -> Integer.compare(u[2], v[2]));
        pq.offer(new int[] {0, 0, 0});
        boolean[] mst = new boolean[n];
        int selectedEdges = 0;
        int cost = 0;
        
        while(pq.size() > 0 || selectedEdges < n - 1) {
            int[] e = pq.poll();
            if(mst[e[1]])
                continue;
            mst[e[1]] = true;
            cost += e[2];
            selectedEdges++;
            for(int j = 0; j < n; j++)
                if(!mst[j])
                    pq.offer(new int[] {e[1], j, dist[e[1]][j]});
        }
        
        return cost;
    }
}
```

***

**Kruskal**

```java
class Solution {
    public int minCostConnectPoints(int[][] p) {
        int n = p.length;
        
        PriorityQueue<int[]> pq = new PriorityQueue<>((u, v) -> Integer.compare(u[2], v[2]));
        for(int i = 0; i < n; i++)
            for(int j = 0; j < n; j++)
                pq.offer(new int[] {i, j, Math.abs(p[i][0] - p[j][0]) + Math.abs(p[i][1] - p[j][1])});
        
        parent = new int[n];
        for (int i = 0; i < n; i++)
            parent[i] = i;  
        
        int selectedEdges = 0;
        int cost = 0;
        
        while (pq.size() > 0 || selectedEdges < n - 1) {
            int[] e = pq.poll();
            int find1 = find(e[0]);
            int find2 = find(e[1]);
            if (find1 == find2) // cycle skip edge
                continue;
            selectedEdges++;
            union(find1, find2);
            cost += e[2];
        }
        
        return cost;
    }
    
    private int[] parent;
    
    private int find(int x) {
        if (parent[x] == x)
            return x;
        return find(parent[x]);
    }

    private void union(int x, int y) {
        int u = find(x);
        int v = find(y);
        if (u != v)
            parent[u] = parent[v];
    }
}
```

***

**Generic Union Find**

Problem Used - [https://leetcode.com/problems/is-graph-bipartite/](https://leetcode.com/problems/is-graph-bipartite/)

```java
class Solution {
    public boolean isBipartite(int[][] graph) {
        UnionFind uf = new UnionFind(graph.length);
        for(int i = 0; i < graph.length; i++) {
            for(int j = 0; j < graph[i].length; j++) {
                if(uf.find(i) == uf.find(graph[i][j]))
                    return false;
                uf.union(graph[i][0], graph[i][j]);
            }
        }
        
        return true;
    }
    
    public class UnionFind {
        private int size;
        private int numComponents; // number of connected components
        private int[] parent;
        private int[] rank;

        public UnionFind(int n) {
            if (n <= 0) throw new IllegalArgumentException("Size <= 0 is not allowed");
            size = numComponents = n;
            parent = new int[n];
            rank = new int[n];
            for (int i = 0; i < n; i++) {
                parent[i] = i;
            }
        }

        public int find(int p) {
            while (p != parent[p]) {
                parent[p] = parent[parent[p]];    // path compression by halving
                p = parent[p];
            }
            return p;
        }

        public void union(int p, int q) {
            int rootP = find(p);
            int rootQ = find(q);

            // These elements are already in the same group!
            if (rootP == rootQ)
                return;

            // Merge smaller component/set into the larger one.
            if (rank[rootQ] > rank[rootP]) {
                parent[rootP] = rootQ;
            } else {
                parent[rootQ] = rootP;
                if (rank[rootP] == rank[rootQ]) {
                    rank[rootP]++;
                }
            }

            // Since the roots found are different we know that the number of components/sets has decreased by one
            numComponents--;
        }

        // Return whether or not the elements 'p' and 'q' are in the same components/set.
        public boolean connected(int p, int q) {
            return find(p) == find(q);
        }

        // Returns the number of remaining components/sets
        public int components() {
            return numComponents;
        }

        // Return the number of elements in this UnionFind/Disjoint set
        public int size() {
            return size;
        }
    }
}
```
