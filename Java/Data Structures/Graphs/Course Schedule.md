### [Course Schedule](https://www.geeksforgeeks.org/problems/course-schedule/1)

## Explanation:
1. **Creating an Adjacency List**: 
    - We start by creating an adjacency list to represent the directed graph. The graph is represented using an ArrayList of ArrayLists, where each inner ArrayList represents the neighbors of a vertex.

2. **Populating the Adjacency List**:
    - We populate the adjacency list based on the given prerequisites. For each prerequisite (u, v), where u is a prerequisite for v, we add v to the list of neighbors of u in the adjacency list.

3. **Calculating Indegree**:
    - We calculate the indegree of each vertex in the graph. The indegree of a vertex is the number of incoming edges to that vertex. This step helps us identify which vertices have no dependencies.

4. **Initializing a Queue**:
    - We initialize a queue to perform Breadth-First Search (BFS) for topological sorting. Initially, we enqueue all vertices with an indegree of 0, as these vertices have no dependencies and can be processed first.

5. **Performing Topological Sorting**:
    - We perform BFS starting from the vertices with an indegree of 0. At each step, we dequeue a vertex and add it to the topological order.
    - For each dequeued vertex, we decrement the indegree of its neighbors since their dependency is satisfied by processing the current vertex.
    - If, after decrementing the indegree, any neighbor's indegree becomes 0, we enqueue that neighbor because its dependencies are satisfied.

6. **Checking for Cycle**:
    - If the number of vertices processed (ind) equals the total number of vertices (n), it means we have successfully obtained a topological order. In this case, we return the topological order.
    - If ind is less than n, it indicates that there is a cycle in the graph. In this case, it's impossible to find a valid topological order, so we return an empty array.

## Time and Space Complexity:
### `Time Complexity`:
- Constructing the adjacency list takes O(n) time.
- Calculating the indegree of each vertex takes O(n + m) time, where m is the number of prerequisites.
- Enqueuing vertices with an indegree of 0 takes O(n) time.
- BFS for topological sorting takes O(n + m) time.
- Overall, the time complexity of the algorithm is O(n + m).
  
### `Space Complexity`:
- The space complexity is dominated by the adjacency list, which requires O(n + m) space to store the graph.
- Additionally, we use arrays and queues of size n for indegrees and BFS, respectively.
- Therefore, the space complexity is O(n + m).
  
## Code:
```java
class Solution {
    // Method to find the topological order
    static int[] findOrder(int n, int m, ArrayList<ArrayList<Integer>> prerequisites) {
        // Create an adjacency list to represent the graph
        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
        // Initialize adjacency list
        for (int i = 0; i < n; i++) {
            adj.add(new ArrayList<>());
        }

        // Populate adjacency list with prerequisites
        for (int i = 0; i < m; i++) {
            adj.get(prerequisites.get(i).get(1)).add(prerequisites.get(i).get(0));
        }

        // Array to store indegree of each vertex
        int indegree[] = new int[n];
        // Calculate indegrees
        for (int i = 0; i < n; i++) {
            for (int it : adj.get(i)) {
                indegree[it]++;
            }
        }

        // Queue to perform BFS for topological sorting
        Queue<Integer> q = new LinkedList<Integer>();
        // Add vertices with indegree 0 to the queue
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0) {
                q.add(i);
            }
        }

        // Array to store the topological order
        int topo[] = new int[n];
        int ind = 0;
        // Perform BFS
        while (!q.isEmpty()) {
            int node = q.peek();
            q.remove();
            topo[ind++] = node; // Add node to topological order

            // Update indegrees and add vertices with indegree 0 to the queue
            for (int it : adj.get(node)) {
                indegree[it]--;
                if (indegree[it] == 0) q.add(it);
            }
        }

        // If topological order is found, return it
        if (ind == n) return topo;
        // If no topological order is possible (graph has a cycle), return an empty array
        int[] arr = {};
        return arr;
    }
}
```
