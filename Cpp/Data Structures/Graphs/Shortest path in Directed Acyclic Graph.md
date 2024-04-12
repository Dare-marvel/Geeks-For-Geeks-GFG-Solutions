### [Shortest path in Directed Acyclic Graph](https://www.geeksforgeeks.org/problems/shortest-path-in-undirected-graph/1)

## Explanation:
### Approach and Intuition of the Main Logic

The given C++ code in the `Solution` class implements the shortest path algorithm for a directed graph using topological sorting. Here's a breakdown of its approach:

#### 1. **Understanding the Components:**
   - **Graph Representation:** The graph is represented using an adjacency list, where each node points to a list of pairs. Each pair contains a destination node and the weight of the edge leading to that node.
   - **Topological Sort:** This sorting method orders the vertices in a directed acyclic graph (DAG) such that for every directed edge \( UV \), vertex \( U \) comes before \( V \) in the ordering.

#### 2. **Topological Sorting Function (`topoSort`):**
   - **Purpose:** This function recursively visits all nodes of the graph in a depth-first search (DFS) manner to produce a stack where nodes are placed after all of their dependencies (or connected nodes) have been placed.
   - **Process:** It marks a node as visited, explores all its unvisited adjacent nodes recursively, and then pushes the node onto a stack. This ensures that a node is pushed only after all nodes reachable from it are already in the stack.

#### 3. **Shortest Path Calculation (`shortestPath`):**
   - **Initialization:** Starts by converting the input edges into an adjacency list. An array to check visited nodes and a stack for the topological sort are initialized.
   - **Topological Sort Invocation:** Traverses all nodes, and for each unvisited node, the `topoSort` function is invoked.
   - **Path Calculation Using Topological Order:**
     - **Distances Initialization:** Before processing, distances from the source node (assumed to be node 0) to all other nodes are set to a large number (simulated infinity), except for the source node itself which is set to zero.
     - **Relaxation:** Nodes are processed in the reverse order of their topological sort. For each node, if there is a shorter path to its adjacent nodes via this node, the distances are updated (relaxed).
   - **Handling Unreachable Nodes:** After processing all nodes, any distances that remain as infinity are set to -1, indicating that those nodes are unreachable from the source.

#### 4. **Complexity:**
   - **Time Complexity:** 
     - The topological sorting of the nodes requires \( O(V + E) \), where \( V \) is the number of vertices and \( E \) is the number of edges, because each vertex and each edge is processed once.
     - Calculating the shortest path also takes \( O(V + E) \) because each node (and its edges) is processed once when taken from the stack.
     - Thus, the total time complexity is \( O(V + E) \).
   - **Space Complexity:** 
     - Space is needed for the adjacency list, visited array, the stack for topological sorting, and the distance array, all of which cumulatively require \( O(V + E) \) space.
     - The adjacency list itself takes \( O(E) \) due to storage of edges, and \( O(V) \) is required for the stack, visited, and distance arrays.

## Code:
```cpp
class Solution {
    
  private:
    // Recursive function to perform topological sorting on the graph
    void topoSort(int node, vector<pair<int, int>> adj[], int vis[], stack<int> &st) {
        vis[node] = 1;  // Mark the current node as visited
        
        // Iterate over all adjacent vertices of the current node
        for (auto it : adj[node]) {
            int v = it.first;
            // If adjacent vertex is not visited, recursively call topoSort on it
            if (!vis[v]) {
                topoSort(v, adj, vis, st);
            }
        }
        
        // All vertices reachable from the current node are processed, push it to the stack
        st.push(node);
    }

  public:
    // Function to find the shortest paths from the source vertex (node 0) to all other vertices
    vector<int> shortestPath(int N, int M, vector<vector<int>>& edges) {
        vector<pair<int, int>> adj[N];  // Adjacency list to store the graph
        
        // Build the graph from the given edge list
        for (int i = 0; i < M; i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            int wt = edges[i][2];
            adj[u].push_back({v, wt});
        }
        
        int vis[N] = {0};  // Array to keep track of visited nodes
        
        stack<int> st;  // Stack to store the topological order of nodes
        
        // Perform topological sorting on all unvisited nodes
        for (int i = 0; i < N; i++) {
            if (!vis[i]) {
                topoSort(i, adj, vis, st);
            }
        }
        
        vector<int> dist(N, 1e9);  // Distance vector initialized to a large number (simulating infinity)
        dist[0] = 0;  // Distance from the source to itself is zero
        
        // Process nodes in topological order
        while (!st.empty()) {
            int node = st.top();  // Get the next node from the topological stack
            st.pop();
            
            // If the distance to the node is not infinity, update distances for all its neighbors
            if (dist[node] != 1e9) {
                for (auto it : adj[node]) {
                    int v = it.first;
                    int wt = it.second;
                    
                    // Relax the edge if a shorter path is found
                    if (dist[node] + wt < dist[v]) {
                        dist[v] = dist[node] + wt;
                    }
                }
            }
        }
        
        // Convert distances of unreachable nodes from infinity to -1
        for (int i = 0; i < N; i++) {
            if (dist[i] == 1e9) dist[i] = -1;
        }
        
        return dist;  // Return the shortest path distances
    }
};
```
