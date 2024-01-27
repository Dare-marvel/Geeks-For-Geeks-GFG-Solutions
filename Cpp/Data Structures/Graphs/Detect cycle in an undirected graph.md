### [Detect cycle in an undirected graph](https://www.geeksforgeeks.org/problems/detect-cycle-in-an-undirected-graph/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=detect-cycle-in-an-undirected-graph)

## [Explanation using BFS](https://takeuforward.org/data-structure/detect-cycle-in-an-undirected-graph-using-bfs/)
## [Explanation using DFS](https://takeuforward.org/data-structure/detect-cycle-in-an-undirected-graph-using-dfs/)


## Code (using DFS):
```cpp
class Solution {
  public:
    bool dfs(int node,int parent, vector<int> adj[],int vis[]){
        vis[node] = 1;
        
        for(auto it: adj[node]){
            if(!vis[it]){
                if(dfs(it,node,adj,vis) == true) return true;
            }
            
            else if(it != parent) return true;
        }
        
        return false;
    }
    // Function to detect cycle in an undirected graph.
    bool isCycle(int V, vector<int> adj[]) {
        int vis[V]={0};
        for(int i=0;i<V;i++){
            if(!vis[i])
                if(dfs(i,-1,adj,vis) == true) return true;
        }
        
        return false;
    }
};
```

## Code (using BFS):
```cpp
// Definition of a class named Solution
class Solution {
public:
    // Function to detect a cycle starting from a given source node in an undirected graph
    bool detectCycle(int src, vector<int> adj[], int vis[]) {
        vis[src] = 1; // Mark the source node as visited

        queue<pair<int, int>> q;
        q.push({src, -1}); // Queue to perform Breadth-First Search (BFS), -1 denotes no parent initially

        while (!q.empty()) {
            int node = q.front().first;
            int parent = q.front().second;
            q.pop();

            // Iterate through the adjacent nodes of the current node
            for (auto it : adj[node]) {
                if (!vis[it]) {
                    vis[it] = 1;
                    q.push({it, node}); // Enqueue the adjacent node with the current node as its parent
                } else if (parent != it) {
                    // If the adjacent node is already visited and not the parent of the current node,
                    // then there is a cycle in the graph
                    return true;
                }
            }
        }

        // No cycle detected
        return false;
    }

    // Function to detect cycle in an undirected graph
    bool isCycle(int V, vector<int> adj[]) {
        int vis[V] = {0}; // Array to mark visited nodes

        // Iterate through each node and check for cycles starting from that node
        for (int i = 0; i < V; i++) {
            if (!vis[i]) {
                if (detectCycle(i, adj, vis)) {
                    return true; // If a cycle is detected, return true
                }
            }
        }

        // No cycle detected in the entire graph
        return false;
    }
};
```
