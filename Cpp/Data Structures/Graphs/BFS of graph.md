### [BFS of graph](https://www.geeksforgeeks.org/problems/bfs-traversal-of-graph/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=bfs_of_graph)

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Code:
```cpp
// Definition of a class named Solution
class Solution {
public:
    // Function to perform Breadth First Traversal of a given graph.
    vector<int> bfsOfGraph(int V, vector<int> adj[]) {
        // Initialize an array to mark visited nodes
        int vis[V+1] = {0};
        
        // Mark the starting node (0 in this case) as visited
        vis[0] = 1;

        // Create a queue for BFS and enqueue the starting node
        queue<int> q;
        q.push(0);

        // Vector to store the result of BFS traversal
        vector<int> bfs;

        // Perform BFS
        while (!q.empty()) {
            // Dequeue a node from the front of the queue
            int node = q.front();
            q.pop();

            // Add the dequeued node to the result
            bfs.push_back(node);

            // Iterate through the adjacent nodes of the dequeued node
            for (auto it : adj[node]) {
                // If the adjacent node is not visited, mark it as visited and enqueue it
                if (!vis[it]) {
                    vis[it] = 1;
                    q.push(it);
                }
            }
        }

        // Return the result of BFS traversal
        return bfs;
    }
};
```
