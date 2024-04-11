### [Prerequisite Tasks](https://www.geeksforgeeks.org/problems/prerequisite-tasks/1)

## Approach and Intuition:
1. **Adjacency List Creation**: The code begins by creating an adjacency list to represent the graph. This list stores the prerequisites for each task. Each task is represented by a node in the graph, and the prerequisites are stored as edges in the graph.
   
2. **Populating the Adjacency List**: Next, the code populates the adjacency list based on the prerequisites provided. It iterates through the given prerequisites array and adds edges to the adjacency list accordingly. This step essentially constructs the graph.

3. **Calculating Indegree**: After constructing the graph, the code calculates the indegree of each node. Indegree represents the number of incoming edges to a node. This is important for identifying the starting nodes for the topological sorting algorithm.

4. **Queue Initialization**: A queue is initialized to perform topological sorting. Nodes with an indegree of 0 (i.e., no incoming edges) are added to the queue initially because these are the nodes that can be processed first without violating any prerequisites.

5. **Topological Sorting**: The main logic of the code lies in performing topological sorting using the queue. The code iteratively removes nodes with an indegree of 0 from the queue, adds them to the topological ordering, and then decreases the indegree of their adjacent nodes. If the indegree of an adjacent node becomes 0 after decrementing, it is added to the queue. This process continues until the queue is empty.

6. **Checking for Successful Sorting**: Finally, the code checks if the size of the topological ordering is equal to the total number of nodes in the graph (N). If they are equal, it indicates that all nodes have been visited and there is no cycle in the graph, implying that it's possible to schedule the tasks according to the given prerequisites. Otherwise, it returns false, indicating that it's not possible to schedule all tasks.

## Time and Space Complexity:
### `Time Complexity`:
- **Adjacency List Creation**: O(N), where N is the number of tasks.
- **Populating the Adjacency List**: O(P), where P is the number of prerequisites.
- **Calculating Indegree**: O(P), where P is the number of prerequisites.
- **Queue Initialization**: O(N), where N is the number of tasks.
- **Topological Sorting**: O(N + P), where N is the number of tasks and P is the number of prerequisites. This is because each node and each edge is visited once.
- **Total Time Complexity**: O(N + P)

### `Space Complexity`:
- **Adjacency List**: O(N + P), where N is the number of tasks and P is the number of prerequisites.
- **Indegree Array**: O(N), where N is the number of tasks.
- **Queue**: O(N), where N is the number of tasks.
- **Topological Ordering List**: O(N), where N is the number of tasks.
- **Total Space Complexity**: O(N + P)

## Code:
```java
class Solution {
    public boolean isPossible(int N, int P, int[][] prerequisites) {
        // Create an adjacency list to represent the graph
        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
        
        // Initialize adjacency list
        for (int i = 0; i < N; i++) {
            adj.add(new ArrayList<>());
        }
        
        // Populate the adjacency list based on prerequisites
        for (int i = 0; i < P; i++) {
            adj.get(prerequisites[i][0]).add(prerequisites[i][1]);
        }
        
        // Calculate indegree of each node
        int[] indegree = new int[N];
        for (int i = 0; i < N; i++) {
            for (int it : adj.get(i)) {
                indegree[it]++;
            }
        }
        
        // Create a queue for topological sorting
        Queue<Integer> q = new LinkedList<Integer>();
        
        // Add nodes with indegree 0 to the queue
        for (int i = 0; i < N; i++) {
            if (indegree[i] == 0) {
                q.add(i);
            }
        }
        
        // Perform topological sorting
        List<Integer> topo = new ArrayList<Integer>();
        while (!q.isEmpty()) {
            int node = q.peek();
            q.remove();
            topo.add(node);
            // Decrease the indegree of adjacent nodes and add them to the queue if their indegree becomes 0
            for (int it : adj.get(node)) {
                indegree[it]--;
                if (indegree[it] == 0) {
                    q.add(it);
                }
            }
        }
        
        // If topological sorting is successful (all nodes visited), return true
        if (topo.size() == N) {
            return true;
        }
        
        // Otherwise, return false
        return false;
    }   
}

```
