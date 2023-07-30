# Graph

When we characterize the running time of a graph algorithm on a given graph $$G = (V, E)$$, we usually measure the size of the input in terms of the number of vertices $$|V|$$and the number of edges $$|E|$$ of the graph.

## Breadth-first search

Time Complexity: O(V+E) where V is number of vertices in the graph and E is number of edges in the graph.

```java
// Java program to print BFS traversal from a given source vertex. 
// BFS(int s) traverses vertices reachable from s. 
import java.io.*; 
import java.util.*; 

// This class represents a directed graph using adjacency list representation 
class Graph 
{ 
	private int V; // No. of vertices 
	private LinkedList<Integer> adj[]; //Adjacency Lists 

	// Constructor 
	Graph(int v) 
	{ 
		V = v; 
		adj = new LinkedList[v]; 
		for (int i=0; i<v; ++i) 
			adj[i] = new LinkedList(); 
	} 

	// Function to add an edge into the graph 
	void addEdge(int v,int w) 
	{ 
		adj[v].add(w); 
	} 

	// prints BFS traversal from a given source s 
	void BFS(int s) 
	{ 
		// Mark all the vertices as not visited(By default set as false) 
		boolean visited[] = new boolean[V]; 

		// Create a queue for BFS 
		LinkedList<Integer> queue = new LinkedList<Integer>(); 

		// Mark the current node as visited and enqueue it 
		visited[s]=true; 
		queue.add(s); 

		while (queue.size() != 0) 
		{ 
			// Dequeue a vertex from queue and print it 
			s = queue.poll(); 
			System.out.print(s+" "); 

			// Get all adjacent vertices of the dequeued vertex s 
			// If a adjacent has not been visited, then mark it visited and enqueue it 
			Iterator<Integer> i = adj[s].listIterator(); 
			while (i.hasNext()) 
			{ 
				int n = i.next(); 
				if (!visited[n]) 
				{ 
					visited[n] = true; 
					queue.add(n); 
				} 
			} 
		} 
	} 

	// Driver method to 
	public static void main(String args[]) 
	{ 
		Graph g = new Graph(4); 

		g.addEdge(0, 1); 
		g.addEdge(0, 2); 
		g.addEdge(1, 2); 
		g.addEdge(2, 0); 
		g.addEdge(2, 3); 
		g.addEdge(3, 3); 

		System.out.println("Following is Breadth First Traversal "+ 
						"(starting from vertex 2)"); 

		g.BFS(2); 
	} 
} 
```

## Depth-first search

&#x20;**Complexity Analysis:**

* **Time complexity:** O(V + E), where V is the number of vertices and E is the number of edges in the graph.
* **Space Complexity:** O(V).\
  Since, an extra visited array is needed of size V.

```java
// Java program to print DFS traversal from a given given graph 
import java.io.*; 
import java.util.*; 

// This class represents a directed graph using adjacency list representation 
class Graph 
{ 
	private int V; // No. of vertices 

	// Array of lists for Adjacency List Representation 
	private LinkedList<Integer> adj[]; 

	// Constructor 
	Graph(int v) 
	{ 
		V = v; 
		adj = new LinkedList[v]; 
		for (int i=0; i<v; ++i) 
			adj[i] = new LinkedList(); 
	} 

	//Function to add an edge into the graph 
	void addEdge(int v, int w) 
	{ 
		adj[v].add(w); // Add w to v's list. 
	} 

	// A function used by DFS 
	void DFSUtil(int v,boolean visited[]) 
	{ 
		// Mark the current node as visited and print it 
		visited[v] = true; 
		System.out.print(v+" "); 

		// Recur for all the vertices adjacent to this vertex 
		Iterator<Integer> i = adj[v].listIterator(); 
		while (i.hasNext()) 
		{ 
			int n = i.next(); 
			if (!visited[n]) 
				DFSUtil(n, visited); 
		} 
	} 

	// The function to do DFS traversal. It uses recursive DFSUtil() 
	void DFS(int v) 
	{ 
		// Mark all the vertices as not visited(set as false by default in java) 
		boolean visited[] = new boolean[V]; 

		// Call the recursive helper function to print DFS traversal 
		DFSUtil(v, visited); 
	} 

	public static void main(String args[]) 
	{ 
		Graph g = new Graph(4); 

		g.addEdge(0, 1); 
		g.addEdge(0, 2); 
		g.addEdge(1, 2); 
		g.addEdge(2, 0); 
		g.addEdge(2, 3); 
		g.addEdge(3, 3); 

		System.out.println("Following is Depth First Traversal "+ 
						"(starting from vertex 2)"); 

		g.DFS(2); 
	} 
} 

```

## Topological sort

**Complexity Analysis:**

* **Time Complexity:** O(V+E).\
  The above algorithm is simply DFS with an extra stack. So time complexity is the same as DFS which is.
* **Auxiliary space:** O(V).\
  The extra space is needed for the stack.

```java
// A Java program to print topological sorting of a DAG 
import java.io.*; 
import java.util.*; 
	
// This class represents a directed graph using adjacency list representation 
class Graph 
{	
	private int V; // No. of vertices 

	// Adjacency List as ArrayList of ArrayList's 
	private ArrayList<ArrayList<Integer>> adj; 
	
	//Constructor 
	Graph(int v) 
	{ 
		V = v; 
		adj = new ArrayList<ArrayList<Integer>>(v); 
		for (int i=0; i<v; ++i) 
			adj.add(new ArrayList<Integer>()); 
	} 
	
	// Function to add an edge into the graph 
	void addEdge(int v,int w) { adj.get(v).add(w); } 
	
	// A recursive function used by topologicalSort 
	void topologicalSortUtil( int v, boolean visited[], Stack<Integer> stack) 
	{ 
		// Mark the current node as visited. 
		visited[v] = true; 
		Integer i; 
	
		// Recur for all the vertices adjacent to thisvertex 
		Iterator<Integer> it = adj.get(v).iterator(); 
		while (it.hasNext()) 
		{ 
			i = it.next(); 
			if (!visited[i]) 
				topologicalSortUtil(i, visited, stack); 
		} 
	
		// Push current vertex to stack which stores result 
		stack.push(new Integer(v)); 
	} 
	
	// The function to do Topological Sort. 
	// It uses recursive topologicalSortUtil() 
	void topologicalSort() 
	{ 
		Stack<Integer> stack = new Stack<Integer>(); 
	
		// Mark all the vertices as not visited 
		boolean visited[] = new boolean[V]; 
		for (int i = 0; i < V; i++) 
			visited[i] = false; 
	
		// Call the recursive helper function to store Topological Sort starting 
		// from all vertices one by one 
		for (int i = 0; i < V; i++) 
			if (visited[i] == false) 
				topologicalSortUtil(i, visited, stack); 
	
		// Print contents of stack 
		while (stack.empty()==false) 
			System.out.print(stack.pop() + " "); 
	} 
	
	// Driver method 
	public static void main(String args[]) 
	{ 
		// Create a graph given in the above diagram 
		Graph g = new Graph(6); 
		g.addEdge(5, 2); 
		g.addEdge(5, 0); 
		g.addEdge(4, 0); 
		g.addEdge(4, 1); 
		g.addEdge(2, 3); 
		g.addEdge(3, 1); 
	
		System.out.println("Following is a Topological " + "sort of the given graph"); 
		g.topologicalSort(); 
	} 
} 

```
