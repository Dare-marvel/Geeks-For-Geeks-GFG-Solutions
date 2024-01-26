### [Number of Provinces](https://www.geeksforgeeks.org/problems/number-of-provinces/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=number_of_provinces)

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

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
