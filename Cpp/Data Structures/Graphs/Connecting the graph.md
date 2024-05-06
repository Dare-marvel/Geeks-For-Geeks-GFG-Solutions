### [Connecting the graph](https://www.geeksforgeeks.org/problems/connecting-the-graph/1)

## **Approach and Intuition:**:

1. **Disjoint Set Data Structure:**
    - The code begins by defining a `DisjointSet` class, which implements the disjoint-set data structure.
    - This data structure is useful for maintaining a collection of disjoint sets and efficiently performing operations like finding the representative of a set and merging sets.
    - It utilizes the concepts of ranks and sizes to optimize union operations and path compression to optimize find operations.

2. **Initialization:**
    - Upon initializing a `DisjointSet` object with size `n`, it initializes three arrays: `rank`, `parent`, and `size`.
    - Each element `i` in the `parent` array initially points to itself, indicating that it's the representative of its own set.
    - Each element in the `size` array is set to 1, indicating the size of each set initially.

3. **Find Operation:**
    - The `findUPar` function is used to find the representative of the set to which a given node belongs.
    - It utilizes path compression by updating the parent of each node along the path to point directly to the representative, which helps in reducing the time complexity of subsequent find operations.

4. **Union Operations:**
    - Two different union operations are defined based on ranks and sizes of sets: `unionByRank` and `unionBySize`.
    - `unionByRank` merges two sets by comparing their ranks. The set with the lower rank is attached to the set with the higher rank. If ranks are equal, one set is attached to the other, and the rank of the resulting set is incremented.
    - `unionBySize` merges two sets by comparing their sizes. The smaller set is attached to the larger set, and the size of the larger set is updated accordingly.

5. **Solution Class:**
    - The `Solution` class contains the main logic to solve the problem.
    - It initializes a `DisjointSet` object with `n` elements and starts processing the given edges.
    - For each edge, it checks if the source and destination vertices belong to the same set using the `findUPar` function.
    - If they belong to the same set, it increments the count of extra edges; otherwise, it merges the sets using the `unionBySize` function.
    - After processing all edges, it counts the number of connected components by counting the number of root nodes in the disjoint set.
    - Finally, it compares the count of extra edges with the count of connected components minus 1. If it's greater than or equal to the latter, it returns the latter minus 1; otherwise, it returns -1.

## Time and Space Complexity:
### `Time Complexity`:
- The time complexity of the `DisjointSet` operations primarily depends on the path compression and union by rank or size operations.
- In the worst-case scenario, where there are `n` elements and `m` union operations, the time complexity is approximately O(n + m * α(n)) for path compression and union by rank, where α(n) is the inverse Ackermann function, which grows very slowly.
- Thus, the overall time complexity of the solution depends on the number of vertices `n` and the number of edges `m`.

### `Space Complexity`:
- The space complexity of the code is O(n), where `n` is the number of elements in the disjoint set.
- This is due to the arrays used to store the rank, parent, and size information for each element in the disjoint set.

## Code:
```cpp
class DisjointSet {
public:
    vector<int> rank, parent, size;

    // Constructor for DisjointSet class, initializes the parent, rank, and size arrays
    DisjointSet(int n) {
        rank.resize(n + 1, 0);  // Resize rank vector and initialize all values to 0
        parent.resize(n + 1);   // Resize parent vector
        size.resize(n + 1);     // Resize size vector
        for (int i = 0; i <= n; i++) {
            parent[i] = i;      // Initialize each element's parent to itself
            size[i] = 1;        // Initialize size of each set to 1
        }
    }

    // Find operation with path compression
    int findUPar(int node) {
        if (node == parent[node])  // If the node is its own parent, return the node
            return node;
        // Otherwise, recursively find the parent and update the parent of the current node
        return parent[node] = findUPar(parent[node]);
    }

    // Union operation by rank
    void unionByRank(int u, int v) {
        int ulp_u = findUPar(u);   // Find the parent of u
        int ulp_v = findUPar(v);   // Find the parent of v
        if (ulp_u == ulp_v) return;    // If u and v are already in the same set, do nothing
        // Union based on ranks of sets
        if (rank[ulp_u] < rank[ulp_v]) {
            parent[ulp_u] = ulp_v;  // Set parent of ulp_u to ulp_v
        }
        else if (rank[ulp_v] < rank[ulp_u]) {
            parent[ulp_v] = ulp_u;  // Set parent of ulp_v to ulp_u
        }
        else {
            parent[ulp_v] = ulp_u;  // Set parent of ulp_v to ulp_u
            rank[ulp_u]++;          // Increment the rank of ulp_u
        }
    }

    // Union operation by size
    void unionBySize(int u, int v) {
        int ulp_u = findUPar(u);   // Find the parent of u
        int ulp_v = findUPar(v);   // Find the parent of v
        if (ulp_u == ulp_v) return;    // If u and v are already in the same set, do nothing
        // Union based on size of sets
        if (size[ulp_u] < size[ulp_v]) {
            parent[ulp_u] = ulp_v;  // Set parent of ulp_u to ulp_v
            size[ulp_v] += size[ulp_u]; // Update the size of ulp_v
        }
        else {
            parent[ulp_v] = ulp_u;  // Set parent of ulp_v to ulp_u
            size[ulp_u] += size[ulp_v]; // Update the size of ulp_u
        }
    }
};

class Solution {
public:
    // Function to solve the problem
    int Solve(int n, vector<vector<int>>& edge) {
        DisjointSet ds(n);  // Create a DisjointSet object with n elements
        
        int cntExtras = 0;  // Counter for extra edges
        
        // Iterate through each edge
        for(auto it: edge){
            int u = it[0];  // Source vertex of edge
            int v = it[1];  // Destination vertex of edge
            
            // If u and v belong to the same set, increment cntExtras
            if(ds.findUPar(u) == ds.findUPar(v)){
                cntExtras++;
            }
            else{  // Otherwise, union the sets of u and v by size
                ds.unionBySize(u,v);
            }
        }
        
        int cntC = 0;  // Counter for connected components
        
        // Iterate through each node
        for(int i=0;i<n;i++) {
            if(ds.parent[i] == i){  // If the node is its own parent, it's a root node of a set
                cntC++;  // Increment the count of connected components
            }
        }
        
        // If the number of extra edges is greater than or equal to the number of connected components minus 1,
        // return the number of connected components minus 1. Otherwise, return -1.
        if(cntExtras >= cntC - 1){
            return cntC -  1;
        }
        
        return -1;
    }
};
```
