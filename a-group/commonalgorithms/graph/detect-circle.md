# Detect circle

### 1. Undirected Graph (DFS)

In an undirected graph, we simply pass the `parent` node during recursion to ensure we don't count the edge we just came from as a "cycle."

```java
import java.util.*;

class Graph {
    private int V;
    private List<List<Integer>> adj;

    public Graph(int v) {
        V = v;
        adj = new ArrayList<>(v);
        for (int i = 0; i < v; i++) adj.add(new ArrayList<>());
    }

    public void addEdge(int u, int v) {
        adj.get(u).add(v);
        adj.get(v).add(u);
    }

    private boolean isCycleUtil(int v, boolean[] visited, int parent) {
        visited[v] = true;

        for (Integer neighbor : adj.get(v)) {
            // If neighbor is not visited, recurse
            if (!visited[neighbor]) {
                if (isCycleUtil(neighbor, visited, v)) return true;
            } 
            // If neighbor is visited and not the parent, cycle found
            else if (neighbor != parent) {
                return true;
            }
        }
        return false;
    }

    public boolean hasCycle() {
        boolean[] visited = new boolean[V];
        for (int i = 0; i < V; i++) {
            if (!visited[i]) {
                if (isCycleUtil(i, visited, -1)) return true;
            }
        }
        return false;
    }
}
```

***

### 2. Directed Graph (BFS / Kahn's Algorithm)

For directed graphs, using In-degrees is the most robust approach. If we can't process all nodes because their in-degrees never reach zero, there must be a cycle.

```java
import java.util.*;

class DirectedGraph {
    private int V;
    private List<List<Integer>> adj;

    public DirectedGraph(int v) {
        V = v;
        adj = new ArrayList<>(v);
        for (int i = 0; i < v; i++) adj.add(new ArrayList<>());
    }

    public void addEdge(int u, int v) {
        adj.get(u).add(v);
    }

    public boolean hasCycle() {
        int[] inDegree = new int[V];
        for (int i = 0; i < V; i++) {
            for (int neighbor : adj.get(i)) inDegree[neighbor]++;
        }

        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < V; i++) {
            if (inDegree[i] == 0) queue.add(i);
        }

        int count = 0;
        while (!queue.isEmpty()) {
            int u = queue.poll();
            count++;

            for (int neighbor : adj.get(u)) {
                if (--inDegree[neighbor] == 0) {
                    queue.add(neighbor);
                }
            }
        }

        // If count doesn't equal V, there's a cycle
        return count != V;
    }
}
```

***

#### Key Takeaways for Java:

* Performance: Both algorithms run in $$ $O(V + E)$ $$ time, where $$ $V$ $$ is vertices and $$ $E$ $$ is edges.
* Space: We use $$ $O(V)$ $$ space for the `visited` array or the `inDegree` array.
* Stack Overflow: For very deep graphs (thousands of nodes), Java's recursive DFS might hit a `StackOverflowError`. In those specific cases, the BFS approach (Kahn's) or an iterative DFS with a manual `Stack` is safer.
