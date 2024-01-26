### [Number of Provinces](https://www.geeksforgeeks.org/problems/number-of-provinces/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=number_of_provinces)

## Explanation:
1. **Class Definition**: The code is encapsulated within a class named `Solution`. This is a common practice in C++ to organize related functions and data together.

2. **DFS Function**: Inside the class, there's a public function `dfs` which takes three parameters: an integer `node` representing the current node, a vector of integers `adjLs[]` representing the adjacency list of the graph, and an integer array `vis[]` to keep track of visited nodes.

3. **DFS Algorithm**: The DFS algorithm starts by marking the current node as visited (`vis[node] = 1`). Then, it iterates over the adjacency list of the current node. If a neighboring node has not been visited, it recursively calls the `dfs` function for that node.

4. **Number of Provinces Function**: There's another public function `numProvinces` which takes two parameters: a 2D vector `adj` representing the adjacency matrix of the graph, and an integer `V` representing the number of vertices in the graph. This function calculates the number of provinces (or connected components) in the graph.

5. **Adjacency List Conversion**: The function first converts the adjacency matrix into an adjacency list `adjLs[]`. For each pair of nodes `i` and `j`, if there's an edge between them (i.e., `adj[i][j] == 1`) and `i` is not equal to `j`, it adds `j` to the adjacency list of `i` and vice versa.

6. **Visited Array Initialization**: The function then initializes the visited array `vis[]` to `0`.

7. **Count Initialization**: The function also initializes a counter `count` to `0`. This counter keeps track of the number of provinces.

8. **DFS Traversal**: The function then starts a DFS traversal from each node `i` that has not been visited. For each such node, it increments the counter `count` and calls the `dfs` function.

9. **Return Statement**: Finally, the function `numProvinces` returns the counter `count`, which is the number of provinces in the graph.

## Time and Space Complexity:
### `Time Complexity`:
The **time complexity** of this code is **O(V^2)**, where `V` is the number of vertices in the graph. This is because each pair of vertices is checked once in the adjacency matrix.

### `Space Complexity`:
The **space complexity** of this code is **O(V + E)**, where `E` is the number of edges in the graph. This is due to the space required for the adjacency list, the visited array, and the call stack for the DFS function.

## Code:
```cpp
// Definition of a class named Solution
class Solution {
public:
    // Recursive function to perform Depth First Search (DFS) starting from a given node
    void dfs(int node, vector<int> adjLs[], int vis[]) {
        vis[node] = 1;

        // Iterate through the adjacent nodes of the current node
        for (auto it : adjLs[node]) {
            // If the adjacent node is not visited, recursively call DFS for that node
            if (!vis[it])
                dfs(it, adjLs, vis);
        }
    }

    // Function to calculate the number of provinces in a given adjacency matrix
    int numProvinces(vector<vector<int>> adj, int V) {
        // Vector to represent an adjacency list
        vector<int> adjLs[V];

        // Convert the given adjacency matrix to an adjacency list
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                if (adj[i][j] == 1 && i != j) {
                    adjLs[i].push_back(j);
                    adjLs[j].push_back(i);
                }
            }
        }

        // Initialize an array to mark visited nodes
        int vis[V] = {0};
        int count = 0;

        // Iterate through each node and perform DFS if not visited
        for (int i = 0; i < V; i++) {
            if (!vis[i]) {
                // Increment count and perform DFS for a new province
                count++;
                dfs(i, adjLs, vis);
            }
        }

        // Return the total count of provinces
        return count;
    }
};
```
