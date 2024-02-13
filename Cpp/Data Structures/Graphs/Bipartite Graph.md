### [Bipartite Graph](https://www.geeksforgeeks.org/problems/bipartite-graph/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=bipartite-graph)

## [Explanation](https://takeuforward.org/graph/bipartite-graph-bfs-implementation/)

## Code (Using BFS):
```cpp
class Solution {
public:
    // Function to check if the graph starting from the given 'start' vertex is bipartite
    bool check(int start, int V, vector<int> adj[], int color[]) {
        // Create a queue for BFS traversal
        queue<int> q;
        q.push(start);

        // Set the color of the starting vertex to 0
        color[start] = 0;

        // Perform BFS traversal
        while (!q.empty()) {
            int node = q.front();
            q.pop();

            // Traverse adjacent vertices
            for (auto it : adj[node]) {
                // If the adjacent vertex has not been colored yet
                if (color[it] == -1) {
                    // Color it with the opposite color of the current node and enqueue it
                    color[it] = !color[node];
                    q.push(it);
                } else if (color[it] == color[node]) {
                    // If the adjacent vertex has the same color as the current node, the graph is not bipartite
                    return false;
                }
            }
        }

        // The graph starting from the given 'start' vertex is bipartite
        return true;
    }

    // Function to check if the entire graph is bipartite
    bool isBipartite(int V, vector<int> adj[]) {
        // Array to store the color of each vertex, initialized to -1 (unvisited)
        int color[V];
        for (int i = 0; i < V; i++)
            color[i] = -1;

        // Iterate through all vertices and check each connected component for bipartiteness
        for (int i = 0; i < V; i++) {
            if (color[i] == -1) {
                // If the current component is not bipartite, return false
                if (check(i, V, adj, color) == false) {
                    return false;
                }
            }
        }

        // The entire graph is bipartite
        return true;
    }
};

```
