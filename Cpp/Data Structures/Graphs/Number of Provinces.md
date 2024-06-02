### [Number of Provinces](https://www.geeksforgeeks.org/problems/number-of-provinces/1)

## Explanation (using Graph Traversal Techniques):
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

## Explanation (using Disjoint Set):
Sure, let's break down the code and understand its logic:

1. **Disjoint Set Data Structure**: The code defines a class `DisjointSet` which is a data structure that keeps track of a partition of a set into disjoint (non-overlapping) subsets. It provides operations for adding new sets, merging sets (replacing them by their union), and finding a representative member of a set. The last operation allows us to determine whether two elements are in the same subset.

2. **Initialization**: In the constructor of `DisjointSet`, we initialize three vectors: `rank`, `parent`, and `size`. Each element is initially in a set of its own, so the `parent` of each element is itself and the `size` of each set is 1. The `rank` is used to keep the tree balanced during union operations and is initially 0.

3. **Find Operation**: The `findUPar` function is used to find the representative member (or the parent) of a set. If an element is the parent of itself, it returns the element. Otherwise, it recursively calls `findUPar` on the parent of the element. This process is called path compression and helps to keep the tree flat which leads to efficient future operations.

4. **Union Operations**: The `unionByRank` and `unionBySize` functions are used to merge two sets. In `unionByRank`, the parent of the smaller rank tree becomes the child of the root of the larger rank tree. If the ranks are the same, we arbitrarily make one the parent of the other and increment the rank of the parent. In `unionBySize`, the parent of the smaller size tree becomes the child of the root of the larger size tree, and the size of the new tree is the sum of the sizes of the two merged trees.

5. **Solution Class**: The `Solution` class uses the `DisjointSet` to solve a problem. The `numProvinces` function takes an adjacency matrix and the number of vertices, and returns the number of provinces (or connected components). It initializes a `DisjointSet` with `V` elements, then iterates over the adjacency matrix. If two vertices are connected, it merges their sets using `unionBySize`. Finally, it counts the number of parents (which represent distinct sets or provinces) and returns this count.

## Time and Space Complexity:
### `Time Complexity`:
The time complexity of this code is **O(V^2)**, where `V` is the number of vertices. This is because we iterate over the adjacency matrix which has `V^2` elements.

### `Space Complexity`:
The space complexity of this code is **O(V)**, where `V` is the number of vertices. This is because we store `V` elements in the `rank`, `parent`, and `size` vectors.

## Code:
```cpp
// Class to represent disjoint sets
class DisjointSet {
    
public:
    // rank[i] is the rank of the i-th set
    // parent[i] is the parent of the i-th set
    // size[i] is the size of the i-th set
    vector<int> rank, parent, size;

    // Constructor to initialize the disjoint sets
    DisjointSet(int n) {
        rank.resize(n + 1, 0);
        parent.resize(n + 1);
        size.resize(n + 1);
        for (int i = 0; i <= n; i++) {
            parent[i] = i; // Initially, each element is its own parent
            size[i] = 1; // Initially, each set has size 1
        }
    }

    // Function to find the ultimate parent of a set
    int findUPar(int node) {
        if (node == parent[node]) // If the node is its own parent, return it
            return node;
        return parent[node] = findUPar(parent[node]); // Else, recursively find the parent
    }

    // Function to merge two sets by rank
    void unionByRank(int u, int v) {
        int ulp_u = findUPar(u); // Find ultimate parent of u
        int ulp_v = findUPar(v); // Find ultimate parent of v
        if (ulp_u == ulp_v) return; // If they are in the same set, return
        if (rank[ulp_u] < rank[ulp_v]) { // If rank of set containing u is less than set containing v
            parent[ulp_u] = ulp_v; // Merge set containing u into set containing v
        }
        else if (rank[ulp_v] < rank[ulp_u]) { // If rank of set containing v is less than set containing u
            parent[ulp_v] = ulp_u; // Merge set containing v into set containing u
        }
        else { // If ranks are equal
            parent[ulp_v] = ulp_u; // Merge set containing v into set containing u
            rank[ulp_u]++; // Increase the rank of set containing u
        }
    }

    // Function to merge two sets by size
    void unionBySize(int u, int v) {
        int ulp_u = findUPar(u); // Find ultimate parent of u
        int ulp_v = findUPar(v); // Find ultimate parent of v
        if (ulp_u == ulp_v) return; // If they are in the same set, return
        if (size[ulp_u] < size[ulp_v]) { // If size of set containing u is less than set containing v
            parent[ulp_u] = ulp_v; // Merge set containing u into set containing v
            size[ulp_v] += size[ulp_u]; // Update the size of the set containing v
        }
        else { // If size of set containing v is less than or equal to set containing u
            parent[ulp_v] = ulp_u; // Merge set containing v into set containing u
            size[ulp_u] += size[ulp_v]; // Update the size of the set containing u
        }
    }
};

// Class to solve the problem
class Solution {
  public:
    // Function to find the number of provinces
    int numProvinces(vector<vector<int>> adj, int V) {
        DisjointSet ds(V); // Initialize the disjoint sets
        
        // For each pair of nodes
        for(int i=0;i<V;i++){
            for(int j=0;j<V;j++){
                // If there is an edge between the nodes
                if(adj[i][j] == 1){
                    // Merge the sets containing the nodes
                    ds.unionBySize(i,j);
                }
            }
        }
        
        int cnt = 0; // Initialize the count of provinces
        for(int i=0;i<V;i++){
            // If the node is its own parent, it is a province
            if(ds.parent[i] == i) cnt++;
        }
        
        return cnt; // Return the count of provinces
    }
};
```
