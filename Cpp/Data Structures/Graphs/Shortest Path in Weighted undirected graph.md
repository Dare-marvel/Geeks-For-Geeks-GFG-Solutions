### [Shortest Path in Weighted undirected graph](https://www.geeksforgeeks.org/problems/shortest-path-in-weighted-undirected-graph/1)

## Explanation:
1. **Initialization**:
   - The code begins by initializing necessary data structures and variables required for Dijkstra's algorithm. This includes:
     - An adjacency list to represent the graph, where each node is associated with its adjacent nodes and corresponding edge weights.
     - Arrays to store the parent nodes and shortest distances from the source node to each node in the graph.
     - A set to keep track of nodes and their corresponding distances, used to prioritize nodes for exploration in Dijkstra's algorithm.
   - The source node (node 1) is initialized with a distance of 0, as the shortest distance from the source to itself is obviously 0.

2. **Building the Graph**:
   - The code iterates through the provided edges and constructs the adjacency list representation of the graph.
   - For each edge, it extracts the source node, destination node, and weight of the edge.
   - It then adds the destination node along with the edge weight to the adjacency list of the source node, and vice versa (since the graph is undirected).

3. **Dijkstra's Algorithm**:
   - The core of the code is the implementation of Dijkstra's algorithm to find the shortest path from the source node to all other nodes in the graph.
   - It repeatedly selects the node with the smallest known distance from the source node from the set.
   - For each selected node, it examines its adjacent nodes and updates their distances if a shorter path is found through the current node.
   - This process continues until all reachable nodes have been processed or until the set becomes empty, indicating that all shortest paths have been determined.

4. **Shortest Path Reconstruction**:
   - After Dijkstra's algorithm completes, the code reconstructs the shortest path from the source node to the target node (node n).
   - It traces back from the target node to the source node using the parent array, which stores the parent of each node along the shortest path.
   - The shortest distance to the target node is also recorded.

5. **Result**:
   - If there is no path from the source node to the target node, indicated by the shortest distance being infinity (1e9 in this case), the code returns -1.
   - Otherwise, it returns the shortest path from the source node to the target node along with the shortest distance.

## Time and Space Complexity:
### `Time Complexity`:
- The time complexity of the provided code is O((n + m) * log(n)), where n is the number of nodes and m is the number of edges in the graph. This complexity arises from the main loop of Dijkstra's algorithm, which iterates over each node and its adjacent edges and performs operations on the set.

### `Space Complexity`:
- The space complexity of the provided code is O(n + m), where n is the number of nodes and m is the number of edges in the graph. This complexity arises from the adjacency list, parent array, and set used for storing nodes and their distances during the execution of Dijkstra's algorithm.
- 
## Code:
```cpp
class Solution {
public:
    vector<int> shortestPath(int n, int m, vector<vector<int>>& edges) {
        // Define an adjacency list to represent the graph
        vector<pair<int,int> > adj[n+1];
        
        // Construct the adjacency list using edges information
        for(int i=0; i<m; i++){
            int u = edges[i][0];  // Source vertex of edge
            int v = edges[i][1];  // Destination vertex of edge
            int wt = edges[i][2]; // Weight of the edge
            
            // For undirected graph, add edge in both directions
            adj[u].push_back({v,wt});  // Add edge from u to v with weight wt
            adj[v].push_back({u,wt});  // Add edge from v to u with weight wt
        }
        
        // Initialize data structures for Dijkstra's algorithm
        vector<int> parent (n+1);          // Store parents of nodes in shortest path
        vector<int> short_dist (n+1,1e9);  // Initialize all distances to infinity
        set<pair<int,int> > st;            // Set to store nodes and their distances
        
        // Start from node 1
        st.insert({0,1});                   // Insert node 1 with distance 0
        short_dist[1] = 0;                  // Distance from source to itself is 0
        for(int i=0; i<=n; i++) parent[i] = i; // Initialize parent array
        
        // Dijkstra's algorithm
        while(!st.empty()){
            auto t = *(st.begin());         // Extract node with minimum distance
            int dist = t.first;             // Extract distance
            int node = t.second;            // Extract node
            st.erase(t);                    // Remove node from set
            
            // Traverse adjacent nodes
            for(auto it : adj[node]){
                int adjNode = it.first;     // Adjacent node
                int weight = it.second;     // Weight of the edge
                
                // Relaxation step
                if( dist + weight < short_dist[adjNode]){
                    if(short_dist[adjNode]!=1e9)
                        st.erase({short_dist[adjNode], adjNode}); // Remove previous distance
                    short_dist[adjNode] = dist + weight;          // Update distance
                    parent[adjNode] = node;                       // Update parent
                    st.insert({short_dist[adjNode],adjNode});     // Insert updated distance
                }
            }
        }
        
        // If there is no path to node n, return -1
        if(short_dist[n] == 1e9) return {-1};
        
        // Reconstruct the shortest path from parent array
        vector<int> ans;
        int node = n;
        while(parent[node]!=node){
            ans.push_back(node);
            node = parent[node];
        }
        ans.push_back(1);                 // Include the source node
        ans.push_back(short_dist[n]);     // Include the shortest distance to node n
        reverse(ans.begin(), ans.end()); // Reverse the path to maintain correct order
        
        return ans; // Return the shortest path
    }
};

```
