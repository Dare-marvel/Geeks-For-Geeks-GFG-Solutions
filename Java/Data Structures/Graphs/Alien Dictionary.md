### [Alien Dictionary](https://www.geeksforgeeks.org/problems/alien-dictionary/1)

## Approach and Intuition::
1. **Topological Sorting**:
    - The main logic of the code revolves around performing topological sorting on a directed acyclic graph (DAG).
    - Topological sorting is a linear ordering of vertices in a graph such that for every directed edge uv from vertex u to vertex v, u comes before v in the ordering.
    - The topological sorting algorithm used in the code ensures that each character comes before its successor character based on the given dictionary order of words.

2. **Constructing the Graph**:
    - The code first constructs a directed graph based on the input dictionary `dict`, where each character is represented as a vertex, and an edge from character 'a' to character 'b' indicates that 'a' comes before 'b' in the dictionary order.
    - It iterates through the given dictionary to find the first character difference between adjacent words, indicating the order relationship between characters.

3. **Performing Topological Sorting**:
    - After constructing the graph, the code uses a standard topological sorting algorithm to find the order of characters.
    - It calculates the indegree of each vertex in the graph to identify the vertices with no incoming edges, i.e., vertices with indegree 0.
    - Starting with the vertices with indegree 0, the code performs a BFS (Breadth-First Search) traversal of the graph, updating the indegree of adjacent vertices as it traverses.
    - The vertices are added to the topological order as they are visited.

4. **Constructing the Result**:
    - After obtaining the topological order of characters, the code constructs the result string by converting the vertex indices to corresponding characters using ASCII representation.

## Time and Space Complexity:
### `Time Complexity`:
- Constructing the graph: O(N * K), where N is the number of words in the dictionary and K is the average length of the words.
- Topological sorting: O(V + E), where V is the number of vertices (characters) and E is the number of edges (order relationships) in the graph.
- Overall time complexity: O(N * K + V + E).

### `Space Complexity`:
- Space required for the adjacency list: O(K) for storing the graph.
- Space required for indegree array: O(V) to store indegree of each vertex.
- Space required for the queue: O(V) for BFS traversal.
- Space required for the topological order: O(V).
- Overall space complexity: O(K + V).
  
## Code:
```java
class Solution {
    
    // Method to perform topological sorting
    private List<Integer> topoSort(int V, List<List<Integer>> adj) {
        // Array to store indegree of each vertex
        int[] indegree = new int[V];
        
        // Calculate indegrees
        for(int i = 0; i < V; i++) {
            for(int it : adj.get(i)) {
                indegree[it]++;
            }
        }
        
        // Queue for BFS
        Queue<Integer> q = new LinkedList<>();
        
        // Enqueue vertices with indegree 0
        for(int i = 0; i < V; i++) {
            if(indegree[i] == 0) {
                q.add(i);
            }
        }
        
        // List to store topological order
        List<Integer> topo = new ArrayList<>();
        
        // Perform BFS
        while(!q.isEmpty()) {
            int node = q.peek();
            q.remove();
            topo.add(node);
            
            // Update indegrees and enqueue vertices with updated indegree 0
            for(int it : adj.get(node)) {
                indegree[it]--;
                if(indegree[it] == 0) 
                    q.add(it);
            }
        }
        
        return topo;
    }
    
    // Method to find the order of characters based on the given dictionary
    public String findOrder(String[] dict, int N, int K) {
        // Adjacency list to represent the graph
        List<List<Integer>> adj = new ArrayList<>();
        
        // Initialize adjacency list
        for(int i = 0; i < K; i++) {
            adj.add(new ArrayList<>());
        }
        
        // Construct the graph based on the dictionary
        for(int i = 0; i < N - 1; i++) {
            String s1 = dict[i];
            String s2 = dict[i + 1];
            
            // Find the first character difference between adjacent words
            int len = Math.min(s1.length(), s2.length());
            for(int ptr = 0; ptr < len; ptr++) {
                if(s1.charAt(ptr) != s2.charAt(ptr)) {
                    adj.get(s1.charAt(ptr) - 'a').add(s2.charAt(ptr) - 'a');
                    break;
                }
            }
        }
        
        // Perform topological sorting
        List<Integer> topo = topoSort(K, adj);
        
        // Construct the result string based on the topological order
        StringBuilder ans = new StringBuilder();
        for(int it : topo) {
            ans.append((char)(it + 'a'));
        }
        
        return ans.toString();
    }
}
```
