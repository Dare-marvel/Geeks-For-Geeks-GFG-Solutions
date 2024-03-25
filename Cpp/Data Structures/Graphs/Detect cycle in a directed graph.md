### [Detect cycle in a directed graph](https://www.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=detect-cycle-in-a-directed-graph)

## [Explanation](https://takeuforward.org/data-structure/detect-cycle-in-a-directed-graph-using-dfs-g-19/):

## Code:
```cpp
class Solution {
  private:
    // Depth-first search function to check for cycles in the graph.
    bool dfsCheck(int node, vector<int> adj[], int vis[], int pathVis[]) {
        // Mark the current node as visited and part of the current path.
        vis[node] = 1;
        pathVis[node] = 1;
        
        // Iterate through the adjacent nodes of the current node.
        for (auto it : adj[node]) {
            // If the adjacent node is not visited, recursively check for cycles.
            if (!vis[it]) {
                if (dfsCheck(it, adj, vis, pathVis) == true) {
                    return true; // If a cycle is found, return true.
                }
            }
            // If the adjacent node is already part of the current path, a cycle is detected.
            else if (pathVis[it]) {
                return true; // Return true indicating the presence of a cycle.
            }
        }
        
        // Once all adjacent nodes are visited, mark the current node as not part of the current path.
        pathVis[node] = 0;
        return false; // Return false indicating no cycle is detected from this node.
    }
  public:
    // Function to detect cycle in a directed graph.
    bool isCyclic(int V, vector<int> adj[]) {
        int vis[V] = {0}; // Array to mark visited nodes.
        int pathVis[V] = {0}; // Array to mark nodes in the current path.
        
        // Iterate through all nodes in the graph.
        for (int i = 0; i < V; i++) {
            // If the node is not visited, start DFS from this node to check for cycles.
            if (!vis[i]) {
                if (dfsCheck(i, adj, vis, pathVis) == true)
                    return true; // If a cycle is found in any DFS traversal, return true.
            }
        }
        
        return false; // If no cycle is found in any traversal, return false.
    }
};

```
