### [Number of Ways to Arrive at Destination](https://www.geeksforgeeks.org/problems/number-of-ways-to-arrive-at-destination/1)

## **Approach and Intuition:**

1. **Graph Representation:**
   - The given graph is represented using an adjacency list. Each node is associated with a list of pairs, where each pair contains the adjacent node and the weight of the edge connecting them.
   - The adjacency list is constructed based on the input roads provided.

2. **Dijkstra's Algorithm:**
   - Dijkstra's algorithm is a greedy algorithm that finds the shortest path from a single source node to all other nodes in a weighted graph.
   - It works by iteratively selecting the node with the shortest distance from the source node and relaxing its neighboring nodes.
   - In this implementation, a priority queue is used to select the node with the minimum distance efficiently.

3. **Initialization:**
   - Initialize a priority queue to store nodes with minimum distance. The priority queue is implemented using a min-heap.
   - Initialize arrays `dist` and `ways` to store the shortest distance from the source node to each node and the number of ways to reach each node, respectively.
   - Initialize the distance of the source node to 0 and the number of ways to reach the source node to 1.

4. **Dijkstra's Algorithm Execution:**
   - Start with the source node and add it to the priority queue with a distance of 0.
   - While the priority queue is not empty, repeat the following steps:
     - Pop the node with the minimum distance from the priority queue.
     - For each neighboring node of the popped node:
       - If a shorter path to the neighboring node is found, update its distance and number of ways to reach it.
       - If another shortest path to the neighboring node is found with the same distance, update the number of ways to reach it by adding the number of ways from the current node.
       - Push the neighboring node into the priority queue if it hasn't been visited yet.

5. **Counting Paths to Destination:**
   - After Dijkstra's algorithm finishes, the number of ways to reach the destination node is stored in the `ways` array at index `n - 1`, where `n` is the total number of nodes.
   - Return the number of ways modulo `1e9 + 7`.

## Time and Space Complexity:
### `Time Complexity`:
- The time complexity of Dijkstra's algorithm with a priority queue implementation is O((V + E) log V), where V is the number of vertices (nodes) and E is the number of edges.
- In this implementation, the main loop iterates through each node and its adjacent edges, and the priority queue operations take O(log V) time.
 
### `Space Complexity`:
- The space complexity is O(V + E), where V is the number of vertices (nodes) and E is the number of edges.
- This space is used to store the adjacency list, the priority queue, and the arrays to store distances and number of ways.

## Code:
```cpp
class Solution {
public:
    // Function to count paths
    int countPaths(int n, vector<vector<int>>& roads) {
        // Create adjacency list to represent graph
        vector<pair<int,int>> adj[n];
        
        // Populate adjacency list from input roads
        for(auto it : roads) {
            adj[it[0]].push_back({it[1], it[2]});
            adj[it[1]].push_back({it[0], it[2]});
        }
        
        // Modulo value for calculations
        int mod = int(1e9 + 7);
        
        // Priority queue to store nodes with minimum distance
        priority_queue<pair<long long,int>, vector<pair<long long,int>>, greater<pair<long long,int>>> q;
        
        // Array to store shortest distances from source to each node
        vector<long long> dist(n, 1e18);
        dist[0] = 0; // Distance from source to itself is 0
        
        // Array to store number of ways to reach each node
        vector<long long> ways(n, 0);
        ways[0] = 1; // There is one way to reach source
        
        // Push source node into priority queue
        q.push({0, 0});
        
        // Dijkstra's algorithm
        while(!q.empty()) {
            int dis = q.top().first; // Current distance
            int node = q.top().second; // Current node
            q.pop(); // Remove current node from queue
            
            // Traverse adjacent nodes
            for(auto it : adj[node]) {
                int adjNode = it.first; // Adjacent node
                long long edW = it.second; // Edge weight to adjacent node
                
                // If a shorter path to adjacent node is found
                if(edW + dis < dist[adjNode]) {
                    dist[adjNode] = edW + dis; // Update shortest distance
                    ways[adjNode] = ways[node]; // Update number of ways
                    
                    // Push adjacent node into priority queue
                    q.push({edW + dis, adjNode});
                }
                // If another shortest path to adjacent node is found
                else if(edW + dis == dist[adjNode]) {
                    ways[adjNode] = (ways[adjNode] + ways[node]) % mod; // Update number of ways
                    // No need to push the adjacent node into priority queue
                    // as it's already present in the queue
                }
            }
        }
        
        // Return number of ways to reach destination
        return ways[n - 1] % mod; // n - 1 is our destination
    }
};
```
