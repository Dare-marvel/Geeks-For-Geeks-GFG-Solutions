### [Cheapest Flights Within K Stops](https://www.geeksforgeeks.org/problems/cheapest-flights-within-k-stops/1)

## Explanation:
1. **Graph Representation:**
   - The code starts by defining a class named `Solution` which contains a method `CheapestFlight`.
   - The method takes five parameters: `n` (number of nodes in the graph), `flights` (a vector of vectors representing directed edges with weights), `src` (source node), `dst` (destination node), and `K` (maximum number of stops allowed).

2. **Initializing Adjacency List:**
   - Inside the method, an adjacency list `adj` is created to represent the graph.
   - Each element of `adj` is a pair representing an adjacent node and the corresponding edge weight.

3. **Building the Graph:**
   - The code iterates over the `flights` vector, which contains information about directed edges and their weights.
   - For each edge, the code adds the destination node and edge weight to the adjacency list of the corresponding source node.

4. **Breadth-First Search (BFS):**
   - The code utilizes BFS to find the shortest path from the source node to the destination node while respecting the maximum number of stops allowed (`K`).
   - It uses a queue to perform BFS traversal.
   - Each element in the queue represents the current node, the number of stops taken to reach that node, and the total cost incurred to reach that node.

5. **Initialization and Relaxation:**
   - The code initializes a distance array `dist` to store the minimum cost to reach each node from the source node. Initially, all distances are set to a large value except for the source node, which is set to 0.
   - During BFS traversal, if a shorter path to a node is found, the distance and cost are updated, and the updated information is added to the queue for further exploration.

6. **Termination and Output:**
   - BFS continues until the queue is empty or until the maximum number of stops (`K`) is exceeded.
   - After BFS completes, if the minimum cost to reach the destination node (`dst`) remains at its initial large value, it indicates that the destination is unreachable within the given constraints. In this case, the method returns -1.
   - Otherwise, the method returns the minimum cost to reach the destination node.

## Time and Space Complexity:
### `Time Complexity`:
- The time complexity of the code is O(V + E), where V is the number of nodes and E is the number of edges in the graph. This complexity arises from the BFS traversal, which visits each node and edge once.
 
### `Space Complexity`:
- The space complexity of the code is O(V), where V is the number of nodes in the graph. This complexity is due to the adjacency list (`adj`), the queue used for BFS traversal, and the distance array (`dist`), all of which require space proportional to the number of nodes in the graph.

## Code:
```cpp
class Solution {
  public:
    // Function to find the cheapest flight from source to destination with at most K stops
    int CheapestFLight(int n, vector<vector<int>>& flights, int src, int dst, int K)  {
        
        // Creating an adjacency list representation of the graph
        vector<pair<int,int>> adj[n];
        
        // Populating the adjacency list
        for(auto it: flights){
            adj[it[0]].push_back({it[1],it[2]});
        }
        
        // Using a queue for BFS traversal, storing {number of stops, {node, cost}}
        queue<pair<int,pair<int,int>>> q;
        q.push({0,{src,0}});
        
        // Initializing distances from source to all nodes to infinity
        vector<int> dist(n,1e9);
        dist[src] = 0;
        
        // BFS traversal
        while(!q.empty()){
            auto it = q.front();
            q.pop();
            
            int stops = it.first;
            int node = it.second.first;
            int cost = it.second.second;
            
            // If number of stops exceeds K, skip this node
            if(stops > K) continue;
            
            // Iterating through adjacent nodes of the current node
            for(auto iter: adj[node]){
                int adjNode = iter.first;
                int edW = iter.second;
                
                // Relaxing the distance if a shorter path is found
                if(cost + edW < dist[adjNode] && stops <= K){
                    dist[adjNode] = cost + edW;
                    // Pushing the updated information into the queue
                    q.push({stops+1,{adjNode,cost+edW}});
                }
            }
        }
        
        // If destination is unreachable, return -1
        if (dist[dst] == 1e9)
            return -1;
        // Otherwise, return the minimum cost to reach the destination
        return dist[dst];
        
    }
};
```
