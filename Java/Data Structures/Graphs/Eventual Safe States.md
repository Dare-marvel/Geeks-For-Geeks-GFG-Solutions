### [Eventual Safe States](https://www.geeksforgeeks.org/problems/eventual-safe-states/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=eventual-safe-states)

## Approach and Intuition:
1. **Problem Statement**: The code is designed to find all the "eventual safe" nodes in a directed graph. A node is considered "eventual safe" if it can reach a terminal node (a node that is not part of any cycle) through any path from it.

2. **Approach**: The code uses Depth-First Search (DFS) to traverse the graph and detect cycles. It maintains three arrays: `vis` for visited nodes, `pathVis` for nodes in the current DFS path, and `check` for nodes already checked for safety.

3. **DFS Function (`dfsCheck`)**: This function checks if a node is part of a cycle. It marks the node as visited (`vis[node] = 1`) and adds it to the current path (`pathVis[node] = 1`). It then iterates over all adjacent nodes. If an adjacent node is not visited, it recursively calls `dfsCheck` for that node. If the recursive call returns `true`, it means a cycle is detected, so it returns `true`. If an adjacent node is already in the current path (`pathVis[it] == 1`), it also means a cycle is detected, so it returns `true`. If no cycle is detected, it marks the node as checked (`check[node] = 1`) and removes it from the current path (`pathVis[node] = 0`), then returns `false`.

4. **Main Function (`eventualSafeNodes`)**: This function initializes the `vis`, `pathVis`, and `check` arrays. It then iterates over all nodes. If a node is not visited, it calls `dfsCheck` for that node. After checking all nodes, it iterates over all nodes again and adds the checked nodes (those not part of any cycle) to the `safeNodes` list.

## Time and Space Complexity:
### `Time Complexity`:
The time complexity of the code is O(V + E), where V is the number of nodes and E is the number of edges. This is because each node and edge is visited once during the DFS traversal.

### `Space Complexity`:
The space complexity of the code is O(V). This is due to the storage required for the `vis`, `pathVis`, and `check` arrays, and the `safeNodes` list, each of which can have at most V elements.

## Code:
```java
class Solution {
    // Depth First Search (DFS) function to check if a node is in a cycle
    private boolean dfsCheck(int node, List<List<Integer>> adj, int vis[], int pathVis[], int check[] ) {
        // Mark the node as visited and in the current path
        vis[node] = 1;
        pathVis[node] = 1;
        // Mark the node as not safe initially
        check[node] = 0;
        
        // Iterate through all adjacent nodes of the current node
        for(int it: adj.get(node)) {
            // If the adjacent node is not visited yet
            if(vis[it] == 0) {
                // Recursively call dfsCheck on the adjacent node
                // If the adjacent node is part of a cycle, return true
                if(dfsCheck(it, adj, vis, pathVis, check)) {
                    return true;
                }
            }
            // If the adjacent node is already visited and is part of the current path
            else if(pathVis[it] == 1) {
                // There's a cycle, return true
                return true;
            }
        }
        
        // Mark the node as safe after exploring all adjacent nodes
        check[node] = 1;
        // Mark the node as not in the current path anymore
        pathVis[node] = 0;
        // Return false indicating no cycle was found
        return false;
    }

    // Function to find the eventual safe nodes in a directed graph
    List<Integer> eventualSafeNodes(int V, List<List<Integer>> adj) {
        // Arrays to track visited nodes, nodes in the current path, and safe nodes
        int [] vis = new int[V];
        int [] pathVis = new int[V];
        int [] check = new int[V];
        
        // Iterate through all nodes in the graph
        for(int i = 0; i < V; i++) {
            // If the node is not visited yet
            if(vis[i] == 0) {
                // Perform depth-first search starting from this node to check for cycles
                dfsCheck(i, adj, vis, pathVis, check);
            }
        }
        
        // Create a list to store the eventual safe nodes
        List<Integer> safeNodes = new ArrayList<>();
        // Iterate through all nodes
        for (int i = 0; i < V; i++) {
            // If the node is marked as safe, add it to the list of safe nodes
            if (check[i] == 1)
                safeNodes.add(i);
        }
        // Return the list of eventual safe nodes
        return safeNodes;
    }
}

```
