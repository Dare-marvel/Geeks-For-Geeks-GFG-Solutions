### [Distance from the Source (Bellman-Ford Algorithm)](https://www.geeksforgeeks.org/problems/distance-from-the-source-bellman-ford-algorithm/1)

## Explanation:
1. **Objective**: The Bellman-Ford algorithm is used to find the shortest paths from a single source vertex to all other vertices in a weighted graph, even when there are negative edge weights.

2. **Initialization**:
   - Initialize a distance vector `dist` of size `V` (number of vertices) with large values, representing infinity. Set the distance of the source vertex `S` to 0, as the distance from the source to itself is always 0.

3. **Relaxation**:
   - The algorithm iterates `V-1` times, relaxing the edges in each iteration.
   - For each edge `(u, v, wt)` in the graph, where `u` is the source vertex, `v` is the destination vertex, and `wt` is the weight of the edge:
     - If the distance to vertex `u` is not infinity (`1e8`) and the distance to `v` through `u` is shorter than the current distance to `v`, update the distance to `v` with the shorter distance (`dist[v] = dist[u] + wt`).

4. **Negative Cycle Detection**:
   - After `V-1` iterations, perform an additional check for negative cycles.
   - If there exists a shorter path to any vertex `v` through vertex `u`, even after `V-1` iterations, then there is a negative cycle in the graph.

5. **Output**:
   - If there are no negative cycles, the `dist` vector will contain the shortest distances from the source vertex `S` to all other vertices in the graph.
   - If there is a negative cycle, return `-1` to indicate its presence.

**Intuition**:

- **Relaxation Principle**: The key principle behind Bellman-Ford is relaxation. In each iteration, it iterates through all edges and relaxes them if a shorter path is found.
- **Correctness**: By iteratively relaxing all edges `V-1` times, the algorithm guarantees that after each iteration, the shortest distance to each vertex is calculated, assuming there are no negative cycles.
- **Negative Cycles**: The additional check after `V-1` iterations is crucial for detecting negative cycles. If there is a negative cycle, the distances to some vertices will keep decreasing infinitely, indicating the presence of a negative cycle.
- **Optimization**: Unlike Dijkstra's algorithm, which works only for non-negative edge weights, Bellman-Ford can handle graphs with negative edge weights. However, it has a higher time complexity.

## Time and Space Complexity:
### `Time Complexity`:
- The time complexity of the Bellman-Ford algorithm is `O(V * E)`, where `V` is the number of vertices and `E` is the number of edges. It iterates through all edges `V-1` times, relaxing each edge in each iteration.

### `Space Complexity`:
- The space complexity is `O(V)`, where `V` is the number of vertices, due to the `dist` vector storing the shortest distances from the source vertex to all other vertices.
 
## Code:
```cpp
class Solution {
public:
    /* Function to implement Bellman Ford algorithm
    *  edges: vector of vectors representing the graph (each inner vector contains three elements: source vertex, destination vertex, and weight of edge)
    *  S: source vertex to start traversing graph from
    *  V: number of vertices in the graph
    */
    vector<int> bellman_ford(int V, vector<vector<int>>& edges, int S) {
        // Initialize distance vector with large values, initially all vertices are unreachable
        vector<int> dist(V, 1e8); // 1e8 represents infinity (large value)
        dist[S] = 0; // Distance to source vertex is set to 0
        
        // Loop V-1 times to relax edges
        for(int i = 0; i < V - 1; i++) {
            // Iterate through each edge
            for(auto it : edges) {
                int u = it[0]; // Source vertex of edge
                int v = it[1]; // Destination vertex of edge
                int wt = it[2]; // Weight of edge
                
                // If a shorter path is found to vertex v through vertex u, update the distance to v
                if(dist[u] != 1e8 && dist[u] + wt < dist[v]) {
                    dist[v] = dist[u] + wt;
                }
            }
        }
        
        // Perform Nth relaxation to check for negative cycles
        for(auto it : edges) {
            int u = it[0]; // Source vertex of edge
            int v = it[1]; // Destination vertex of edge
            int wt = it[2]; // Weight of edge
            
            // If a shorter path is found to vertex v through vertex u, then there is a negative cycle
            if(dist[u] != 1e8 && dist[u] + wt < dist[v]) {
                return { -1 }; // Return -1 to indicate the presence of a negative cycle
            }
        }
        
        return dist; // Return the vector containing distances from source vertex to all other vertices
    }
};
```
