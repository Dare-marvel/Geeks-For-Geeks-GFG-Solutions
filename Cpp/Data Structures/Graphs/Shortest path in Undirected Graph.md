### [Shortest path in Undirected Graph](https://www.geeksforgeeks.org/problems/shortest-path-in-undirected-graph-having-unit-distance/1)

## [Approach and Intuition of the Main Logic](https://takeuforward.org/data-structure/shortest-path-in-undirected-graph-with-unit-distance-g-28/):

The provided C++ code in the `Solution` class demonstrates how to find the shortest path distances from a given source node to all other nodes in an undirected and unweighted graph using the Breadth-First Search (BFS) algorithm. Let's explore the key components and intuition behind this implementation:

#### Graph Representation
- **Adjacency List:** The graph is represented using an adjacency list `adj`, where `adj[i]` contains a list of nodes directly connected to node `i`. This representation is space-efficient and well-suited for BFS.

#### Building the Graph
- **Input Edges:** The function accepts a list of edges, where each edge is represented as a vector containing two integers. For an undirected graph, each edge `(u, v)` implies a connection from `u` to `v` and vice versa.
- **Populating Adjacency List:** The adjacency list is populated in a loop where each edge is processed to add both connections due to the undirected nature of the graph.

#### BFS Initialization
- **Distance Vector:** A vector `dist` of size `N` (number of nodes) is initialized with a high value (`1e9`) for all nodes. This high value acts as an indicator of "infinity," suggesting that initially, all nodes are considered unreachable.
- **Source Node:** The distance to the source node is set to 0 because the shortest path to itself is always zero.
- **Queue:** A queue `q` is used to manage the nodes during BFS traversal. The source node is enqueued first.

#### BFS Traversal
- **Process Nodes:** Nodes are dequeued one by one, and for each node, its adjacent nodes are examined.
- **Updating Distances:** If the distance to an adjacent node through the current node is shorter than its previously recorded distance, it is updated and the adjacent node is enqueued for further exploration. This step ensures that nodes are explored layer by layer, maintaining the shortest path property of BFS.

#### Final Adjustments
- **Handling Unreachable Nodes:** After BFS traversal, nodes that still have their distance set as `1e9` are updated to `-1`, indicating that these nodes are not reachable from the source node.

## Time and Space Complexity

### `Time Complexity`
- **O(N + M):** Each node and each edge in the graph is processed at most once. Building the adjacency list requires iterating over all edges, contributing O(M) complexity. During BFS, each node is dequeued once (O(N)), and for each node, all its adjacent edges are processed once (O(M) over all nodes). Hence, the total time complexity of the algorithm is O(N + M).

### `Space Complexity`
- **O(N + M):**
  - **Adjacency List:** Takes O(N + M) space as each edge contributes twice to the list (once for each direction in an undirected graph).
  - **Distance Vector:** O(N) for storing distances of N nodes.
  - **Queue:** In the worst case, the queue could hold all nodes simultaneously in scenarios where most nodes are in the same layer, contributing additional O(N).
  - **Overall:** The space complexity sums up to O(N + M).

## Code:
```cpp
class Solution {
  public:
    // Function to find the shortest path distances from the source node to all other nodes in an unweighted graph
    vector<int> shortestPath(vector<vector<int>>& edges, int N, int M, int src){
        // adj represents the adjacency list of the graph where N is the number of nodes
        vector<int> adj[N];
        
        // Build the graph from the given list of edges
        for(auto it: edges){
            adj[it[0]].push_back(it[1]); // Add edge from it[0] to it[1]
            adj[it[1]].push_back(it[0]); // Since the graph is undirected, add edge from it[1] to it[0] as well
        }
        
        // dist array to store the distance from the source to each node, initialized to a large value (1e9 here simulates infinity)
        vector<int> dist(N);
        for(int i = 0; i < N; i++) dist[i] = 1e9;
        
        // Set the distance to the source node as 0
        dist[src] = 0;
        
        // Queue to manage the BFS process
        queue<int> q;
        q.push(src); // Start BFS from the source node
        
        // BFS algorithm
        while(!q.empty()){
            int node = q.front(); // Get the front node from the queue
            q.pop(); // Remove that node from the queue
            
            // Explore all adjacent nodes
            for(auto it: adj[node]){
                // If the current path offers a shorter distance to the adjacent node, update it and push to queue
                if(dist[node] + 1 < dist[it]){
                    dist[it] = dist[node] + 1; // Update the distance
                    q.push(it); // Push the updated node into the queue for further exploration
                }
            }
        }
        
        // Handling unreachable nodes: Set their distance to -1
        for(int i = 0; i < N; i++){
            if(dist[i] == 1e9){
                dist[i] = -1;
            }
        }
        
        // Return the array of distances
        return dist;
    }
};
```
