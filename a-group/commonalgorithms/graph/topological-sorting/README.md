# Topological Sort

[Topological Sorting](broken-reference)

> 拓扑排序是一个dfs的应用, 所谓拓扑排序是指在一个DAG(有向无回路图)里给每个节点定义一个顺序(v1…vn), 使得按照这个顺序遍历的节点, 每一个节点vi都是之前遍历过的的节点(v1 \~ vi-1)所指向的(或没有任何其他节点指向的).

See:

* [Course Schedule](broken-reference)
* [Course Schedule II](broken-reference)

## Problem

Given an directed graph, a topological order of the graph nodes is defined as follow:&#x20;

* For each directed edge A -> B in graph, A must before B in the order list.&#x20;
* The first node in the order can be any node in the graph with no nodes direct to it.&#x20;

Find any topological order for the given graph.

## Solution

```java
/**
 * Definition for Directed graph.
 * class DirectedGraphNode {
 *     int label;
 *     ArrayList<DirectedGraphNode> neighbors;
 *     DirectedGraphNode(int x) 
 *      { label = x; neighbors = new ArrayList<DirectedGraphNode>(); }
 * };
 */
 // Recursive Solution
public class Solution {
    /**
     * @param graph: A list of Directed graph node
     * @return: Any topological order for the given graph.
     ***/    
    public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
        ArrayList<DirectedGraphNode> res = 
		new ArrayList<DirectedGraphNode>();
        if(graph == null || graph.size() == 0) return res;
        
        Map<DirectedGraphNode, Integer> map = 
		new HashMap<DirectedGraphNode, Integer>();
        for(DirectedGraphNode node : graph){
            map.put(node, 0);
        }
        for(DirectedGraphNode node : graph){
            if(map.get(node) == 0)
        	    findASort(graph, node, map, res);
        }
        return res;
    }
    
    void findASort(ArrayList<DirectedGraphNode> graph, DirectedGraphNode node,    
                 Map<DirectedGraphNode, Integer> map, ArrayList<DirectedGraphNode> res){
        map.put(node, 1);
        for(DirectedGraphNode nb : node.neighbors){
            if(map.get(nb) == 0)
                findASort(graph, nb, map, res);
        }
        res.add(0, node);
    }
}

// Iterative Solution
public class Solution {
    /*
     * @param graph: A list of Directed graph node
     * @return: Any topological order for the given graph.
     */
    public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
        ArrayList<DirectedGraphNode> order = new ArrayList<>();
        Map<DirectedGraphNode, Integer> indegree = new HashMap<>();
        for (DirectedGraphNode node : graph) {
            for (DirectedGraphNode neighbor : node.neighbors) {
                if (indegree.containsKey(neighbor)) {
                    indegree.put(neighbor, indegree.get(neighbor) + 1);
                } else {
                    indegree.put(neighbor, 1);
                }
            }
        }
        
        Queue<DirectedGraphNode> queue = new ArrayDeque<>();
        for (DirectedGraphNode node : graph) {
            if (!indegree.containsKey(node)) {
                queue.offer(node);
                order.add(node);
            }
        }
        
        while (!queue.isEmpty()) {
            DirectedGraphNode node = queue.poll();
            for (DirectedGraphNode neighbor : node.neighbors) {
                indegree.put(neighbor, indegree.get(neighbor) - 1);
                if (indegree.get(neighbor) == 0) {
                    order.add(neighbor);
                    queue.offer(neighbor);
                }
            }
        }
        
        return order;
    }
}

```

## Topological Sort Template -- General Approach!!

`Topological Sort is Easy` -- The General Template\
\*\
**What we need ?**\
`1. HashMap<Node, Indegree> inDegree`: A in-degree map, which record each nodes in-degree.\
`2. HashMap<Node, List<Node>children> topoMap`: A topo-map which record the Node's children

**What we do ?**\
`1. Init`: Init the two HashMaps.\
`2. Build Map`: Put the child into parent's list ; Increase child's in-degree by 1.\
`3. Find Node with 0 in-degree`: Iterate the inDegree map, find the Node has 0 inDegree. (If none, there must be a circle)\
`4. Decrease the children's inDegree by 1`: Decrease step3's children's inDegree by 1.\
`5. Remove this Node`: Remove step3's Node from inDegree. Break current iteration.\
`6. Do 3-5 until inDegree is Empty`: Use a while loop
