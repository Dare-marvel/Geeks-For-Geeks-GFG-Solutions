### [Topological sort](https://www.geeksforgeeks.org/problems/topological-sort/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=topological-sort)

## Approach and Intuition:
1. **Depth-First Search (DFS):**
   - The main logic of the code utilizes Depth-First Search (DFS) traversal to generate the topological ordering of vertices in a directed acyclic graph (DAG).
   - DFS is a graph traversal algorithm that explores as far as possible along each branch before backtracking.

2. **Topological Sorting:**
   - Topological sorting is a linear ordering of vertices in a directed graph where for every directed edge uv from vertex u to vertex v, u comes before v in the ordering.
   - It's crucial to understand that topological sorting is only possible in Directed Acyclic Graphs (DAGs).

3. **DFS Implementation:**
   - The `dfs` function is a recursive implementation of DFS.
   - It takes four parameters: the current node, the array to track visited nodes, a stack to store visited nodes in reverse order, and the adjacency list representing the graph.
   - It marks the current node as visited and recursively explores all unvisited neighbors of the current node.

4. **Visited Array:**
   - The `vis` array keeps track of visited nodes to avoid revisiting already visited nodes during DFS traversal.
   - Initially, all elements of `vis` are set to 0, indicating that no nodes have been visited yet.

5. **Stack for Topological Ordering:**
   - The `st` stack is used to store vertices in reverse topological order.
   - After visiting all the neighbors of a node in DFS, the node is pushed onto the stack.

6. **Topological Sorting Function:**
   - The `topoSort` function initializes the visited array and stack.
   - It iterates through each vertex and performs DFS on unvisited vertices.
   - As a result of DFS, the stack contains vertices in reverse topological order.

7. **Retrieving Topological Ordering:**
   - Once DFS traversal is complete, vertices are popped from the stack one by one.
   - The popped vertices constitute the topological ordering of the graph.

## Time and Space Complexity:
### `Time Complexity`:
- The time complexity of the DFS traversal is O(V + E), where V is the number of vertices and E is the number of edges in the graph.
- The overall time complexity of the topological sorting algorithm is also O(V + E), as it involves a single DFS traversal.
  
### `Space Complexity`:
- The space complexity is O(V + E) as well.
- It's dominated by the space required for the adjacency list (O(V + E)), the visited array (O(V)), and the stack (O(V)).
  
## Code:
```java
class Solution {
    // Private method for performing depth-first search (DFS) traversal
    // to generate topological ordering of vertices.
    private static void dfs(int node, int vis[], Stack<Integer> st,
                            ArrayList<ArrayList<Integer>> adj) {
        // Mark the current node as visited
        vis[node] = 1;
        
        // Traverse through all adjacent nodes of the current node
        for (int it : adj.get(node)) {
            // If the adjacent node hasn't been visited, perform DFS on it
            if (vis[it] == 0)
                dfs(it, vis, st, adj);
        }
        
        // Push the current node onto the stack after visiting all its neighbors
        st.push(node);
    }

    // Function to return a list containing vertices in topological order.
    static int[] topoSort(int V, ArrayList<ArrayList<Integer>> adj) {
        // Array to track visited status of each vertex
        int vis[] = new int[V];
        
        // Stack to store vertices in reverse topological order
        Stack<Integer> st = new Stack<Integer>();
        
        // Iterate through each vertex
        for (int i = 0; i < V; i++) {
            // If the vertex hasn't been visited, perform DFS on it
            if (vis[i] == 0) {
                dfs(i, vis, st, adj);
            }
        }

        // Array to store the final topological ordering of vertices
        int ans[] = new int[V];
        
        // Index to track the position in the ans array
        int i = 0;
        
        // Pop vertices from the stack to retrieve topological order
        while (!st.isEmpty()) {
            ans[i++] = st.peek();
            st.pop();
        }
        
        // Return the topological ordering of vertices
        return ans;
    }
}

```
