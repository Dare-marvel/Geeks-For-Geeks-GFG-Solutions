### [BFS of graph](https://www.geeksforgeeks.org/problems/bfs-traversal-of-graph/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=bfs_of_graph)

## Explanation:
1. **Class Definition**: The code is encapsulated within a class named `Solution`. This is a common practice in C++ to organize related functions and data together.

2. **Function Declaration**: Inside the class, there's a public function `bfsOfGraph` which takes two parameters: an integer `V` representing the number of vertices in the graph, and a vector of integers `adj[]` representing the adjacency list of the graph.

3. **Visited Array**: Inside the function, an array `vis` of size `V+1` is declared and initialized to `0`. This array keeps track of the nodes that have been visited in the graph.

4. **Queue Declaration**: A queue `q` is declared. This queue is used to store the nodes of the graph as they are visited.

5. **BFS Vector**: A vector `bfs` is declared. This vector stores the nodes in the order they are visited, which is the Breadth-First Search (BFS) traversal of the graph.

6. **BFS Algorithm**: The BFS algorithm starts by marking the first node (node `0`) as visited (`vis[0] = 1`) and pushing it into the queue (`q.push(0)`). Then, it enters a while loop that continues until the queue is empty. Inside the loop, it pops the front node from the queue and pushes it into the `bfs` vector. Then, it iterates over the adjacency list of the current node. If a neighboring node has not been visited, it is marked as visited and pushed into the queue.

7. **Return Statement**: Finally, the function returns the `bfs` vector, which is the BFS traversal of the graph.

## Time and Space Complexity:
### `Time Complexity`:
The **time complexity** of this code is **O(V + E)**, where `V` is the number of vertices and `E` is the number of edges in the graph. This is because each vertex and each edge is visited exactly once in the BFS traversal.

### `Space Complexity`:
The **space complexity** of this code is also **O(V + E)**, due to the space required for the adjacency list, the queue, and the visited array. The BFS vector also requires space, but it is not counted in the space complexity as it is the output of the function.

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
