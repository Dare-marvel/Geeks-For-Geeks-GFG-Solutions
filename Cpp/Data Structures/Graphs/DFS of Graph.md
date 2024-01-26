### [DFS of Graph](https://www.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=dfs_of_graph)

## Explanation:
Sure, here's an explanation of the code:

1. **Class Definition**: The code is encapsulated within a class named `Solution`. This is a common practice in C++ to organize related functions and data together.

2. **DFS Function**: Inside the class, there's a public function `dfs` which takes four parameters: an integer `node` representing the current node, a vector of integers `adj[]` representing the adjacency list of the graph, an integer array `vis[]` to keep track of visited nodes, and a vector `ls` to store the DFS traversal.

3. **DFS Algorithm**: The DFS algorithm starts by marking the current node as visited (`vis[node] = 1`) and adding it to the DFS list (`ls.push_back(node)`). Then, it iterates over the adjacency list of the current node. If a neighboring node has not been visited, it recursively calls the `dfs` function for that node.

4. **DFS Traversal Function**: There's another public function `dfsOfGraph` which takes two parameters: an integer `V` representing the number of vertices in the graph, and a vector of integers `adj[]` representing the adjacency list of the graph. This function initializes the visited array `vis[]` and the DFS list `ls`, and starts the DFS traversal from the node `0` by calling the `dfs` function.

5. **Return Statement**: Finally, the function `dfsOfGraph` returns the `ls` vector, which is the DFS traversal of the graph.

## Time and Space Complexity:
### `Time Complexity`:
The **time complexity** of this code is **O(V + E)**, where `V` is the number of vertices and `E` is the number of edges in the graph. This is because each vertex and each edge is visited exactly once in the DFS traversal.

### `Space Complexity`:
The **space complexity** of this code is also **O(V + E)**, due to the space required for the adjacency list, the visited array, and the DFS list.

## Code:
```cpp
// Definition of a class named Solution
class Solution {
public:
    // Recursive function to perform Depth First Search (DFS) starting from a given node
    void dfs(int node, vector<int> adj[], int vis[], vector<int> &ls) {
        // Mark the current node as visited
        vis[node] = 1;

        // Add the current node to the DFS traversal list
        ls.push_back(node);

        // Iterate through the adjacent nodes of the current node
        for (auto it : adj[node]) {
            // If the adjacent node is not visited, recursively call DFS for that node
            if (!vis[it]) {
                dfs(it, adj, vis, ls);
            }
        }
    }

    // Function to return a list containing the DFS traversal of the graph.
    vector<int> dfsOfGraph(int V, vector<int> adj[]) {
        // Initialize an array to mark visited nodes
        int vis[V+1] = {0};
        
        // Choose a starting node (0 in this case)
        int start = 0;

        // Vector to store the result of DFS traversal
        vector<int> ls;

        // Call the DFS function starting from the chosen node
        dfs(start, adj, vis, ls);

        // Return the result of DFS traversal
        return ls;
    }
};

```
