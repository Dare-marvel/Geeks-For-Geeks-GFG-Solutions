### [Implementing Dijkstra Algorithm](https://www.geeksforgeeks.org/problems/implementing-dijkstra-set-1-adjacency-matrix/1)

## Approach and Intuition::
1. **Understanding Dijkstra's Algorithm**:
   - Dijkstra's algorithm is a popular method for finding the shortest paths between nodes in a weighted graph.
   - It works by iteratively exploring the vertices of the graph, always selecting the vertex with the smallest known distance from the source vertex.
   - As it progresses, it updates the distances to neighboring vertices if it finds shorter paths.

2. **Priority Queue for Vertex Selection**:
   - The algorithm employs a priority queue to select the next vertex to explore.
   - The priority queue stores pairs of (distance, vertex) tuples, with the priority based on the distance.
   - This ensures that the algorithm always explores vertices with the smallest known distance first.

3. **Initialization**:
   - Initialize a priority queue (`pq`) to store vertex-distance pairs. It's a min-heap, so the smallest distance vertex is always at the top.
   - Initialize a vector `distTo` to store the shortest distances from the source vertex to all other vertices. Initialize all distances to infinity except the source vertex, which is set to 0.
   - Push the source vertex (`S`) with distance 0 into the priority queue.

4. **Main Loop**:
   - While the priority queue is not empty, continue the loop.
   - Extract the vertex (`node`) with the smallest distance (`dis`) from the priority queue.
   - For each neighboring vertex `v` of the extracted vertex, check if the distance from the source to `v` through `node` is shorter than the currently known distance.
   - If it is, update the distance to `v` and push it into the priority queue with the updated distance.
   - Continue this process until all vertices are explored.

5. **Updating Shortest Distances**:
   - When considering a neighboring vertex `v`, if the path through the extracted vertex `node` is shorter than the current known distance to `v`, update the distance to `v` and push it into the priority queue.
   - This ensures that the algorithm gradually discovers shorter paths as it explores the graph.

## Time and Space Complexity:
### `Time Complexity`:
- The time complexity of Dijkstra's algorithm depends on the data structures used and the size of the graph.
- Let \( V \) be the number of vertices and \( E \) be the number of edges in the graph.
- In each iteration of the main loop, the algorithm extracts the vertex with the smallest distance from the priority queue, which takes \( O(\log V) \) time.
- Each edge is examined at most once, so the overall time complexity is \( O((V + E) \log V) \).

### `Space Complexity`:
- The space complexity primarily depends on the size of the priority queue and the size of the `distTo` vector.
- Both of these data structures can have a maximum size of \( O(V) \).
- Therefore, the space complexity is \( O(V) \).

## Code:
```cpp
class Solution
{
public:
    // Function to find the shortest distance of all the vertices
    // from the source vertex S using Dijkstra's algorithm.
    vector <int> dijkstra(int V, vector<vector<int>> adj[], int S)
    {
        // Priority queue to store pairs of distance and vertex,
        // sorted by distance in ascending order.
        priority_queue <pair<int,int>, vector<pair<int,int>>, greater<pair<int,int>>> pq;
        
        // Initialize a vector to store the shortest distances from the source vertex.
        // Initialize all distances to infinity initially.
        vector<int> distTo(V,INT_MAX);
        
        // Distance to the source vertex is 0.
        distTo[S] = 0;
        
        // Push the source vertex and its distance (0) into the priority queue.
        pq.push({0,S});
        
        // Dijkstra's algorithm
        while(!pq.empty()){
            // Extract the vertex with the smallest distance from the priority queue.
            int node = pq.top().second;
            int dis = pq.top().first;
            pq.pop();
            
            // Traverse all adjacent vertices of the extracted vertex.
            for(auto it: adj[node]){
                int v = it[0];  // Adjacent vertex
                int w = it[1];  // Weight of the edge from 'node' to 'v'
                
                // If the new calculated distance to 'v' is smaller than the current distance,
                // update the distance to 'v' and push it into the priority queue.
                if(dis + w < distTo[v]){
                    distTo[v] = dis + w;
                    pq.push({dis+w,v});
                }
            }
        }
        
        // Return the vector containing the shortest distances from the source vertex.
        return distTo;
    }
};
```
