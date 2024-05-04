### [Minimum Spanning Tree](https://www.geeksforgeeks.org/problems/minimum-spanning-tree/1)

## Prim's Algorithm:
1. **Priority Queue Initialization**:
   - A priority queue is initialized to store pairs of (weight, node) in ascending order of weight.
   - The priority queue is configured to prioritize elements with smaller weights.

2. **Visited Array Initialization**:
   - An array `vis` is initialized to keep track of visited nodes.
   - Initially, all nodes are marked as not visited (0).

3. **Starting Node Initialization**:
   - The starting node (node 0) is pushed into the priority queue with weight 0.
   - This initiates the algorithm from the starting node.

4. **Main Loop**:
   - The algorithm iterates until the priority queue becomes empty.
   - In each iteration, it extracts the node with the minimum weight from the priority queue.

5. **Node Extraction**:
   - The pair (weight, node) is extracted from the priority queue.
   - The weight represents the weight of the edge connecting the current node to its parent node.
   - The node represents the current node being processed.

6. **Node Visitation Check**:
   - If the current node is already visited, it is skipped, and the algorithm proceeds to the next iteration.
   - This check ensures that each node is visited only once.

7. **Node Visitation and Weight Addition**:
   - If the current node is not visited, it is marked as visited.
   - The weight of the current edge is added to the total sum of edge weights.

8. **Neighbor Exploration**:
   - The algorithm explores all adjacent nodes of the current node.
   - For each adjacent node:
     - If the adjacent node is not visited, the edge weight between the current node and the adjacent node is added to the priority queue.
     - This ensures that the algorithm considers all possible edges while constructing the minimum spanning tree.

9. **Sum Calculation**:
   - After processing all edges, the sum of weights of edges in the minimum spanning tree is returned.

**Approach and Intuition**:
- The algorithm is based on Prim's algorithm, which constructs a minimum spanning tree by iteratively adding the smallest edge that connects a vertex in the growing tree to a vertex outside the tree.
- By maintaining a priority queue of edges, the algorithm efficiently selects the smallest edge to expand the tree.
- The use of a visited array ensures that each node is visited only once, preventing cycles in the spanning tree.
- By exploring all adjacent nodes of each visited node, the algorithm guarantees that the minimum spanning tree spans all vertices of the graph.

## Time and Space Complexity:
### **Time Complexity**:
- The time complexity of the algorithm depends on the number of vertices (V) and edges (E) in the graph.
- In each iteration, extracting the minimum edge from the priority queue takes O(log V) time.
- Exploring adjacent nodes of each vertex takes O(E) time in total.
- Overall, the time complexity is O(V log V + E log V).

### **Space Complexity**:
- The space complexity is dominated by the priority queue and the visited array.
- The priority queue can store at most V elements, resulting in O(V) space.
- The visited array also requires O(V) space.
- Therefore, the space complexity is O(V).

## Code:
```cpp
class Solution
{
	public:
	// Function to find sum of weights of edges of the Minimum Spanning Tree.
    int spanningTree(int V, vector<vector<int>> adj[])
    {
        // Priority queue to store pairs of (weight, node) in increasing order of weight.
        priority_queue<pair<int,int>, vector<pair<int,int>>, greater<pair<int,int>> > pq;
        
        // Array to keep track of visited nodes.
        vector<int> vis(V,0);
        
        // Pushing the source node (node 0) with weight 0 into the priority queue.
        pq.push({0,0});
        
        // Variable to store the sum of weights of edges in the Minimum Spanning Tree.
        int sum = 0;
        
        // Loop until priority queue is not empty.
        while(!pq.empty()){
            // Extract the node with the minimum weight from the priority queue.
            auto it = pq.top();
            pq.pop();
            int node = it.second; // Extracted node.
            int wt = it.first; // Weight of the edge.
            
            // If node is already visited, skip it.
            if(vis[node] == 1) continue;
            
            // Mark the current node as visited and add its weight to the total sum.
            vis[node] = 1;
            sum += wt;
            
            // Iterate over all adjacent nodes of the current node.
            for(auto it: adj[node]){
                int adjNode = it[0]; // Adjacent node.
                int edW = it[1]; // Weight of the edge connecting current node and adjacent node.
                
                // If adjacent node is not visited, push it into the priority queue.
                if(!vis[adjNode]){
                    pq.push({edW,adjNode});
                }
                
            }
        }
        
        // Return the sum of weights of edges in the Minimum Spanning Tree.
        return sum;
    }
};
```

<hr> 

## [Explanation](https://takeuforward.org/data-structure/kruskals-algorithm-minimum-spanning-tree-g-47/)

## Code (Kruskal's Algorithm):
```cpp
class DisjointSet {
    vector<int> rank, parent, size;
public:
    DisjointSet(int n) {
        rank.resize(n + 1, 0);
        parent.resize(n + 1);
        size.resize(n + 1);
        for (int i = 0; i <= n; i++) {
            parent[i] = i;
            size[i] = 1;
        }
    }

    int findUPar(int node) {
        if (node == parent[node])
            return node;
        return parent[node] = findUPar(parent[node]);
    }

    void unionByRank(int u, int v) {
        int ulp_u = findUPar(u);
        int ulp_v = findUPar(v);
        if (ulp_u == ulp_v) return;
        if (rank[ulp_u] < rank[ulp_v]) {
            parent[ulp_u] = ulp_v;
        }
        else if (rank[ulp_v] < rank[ulp_u]) {
            parent[ulp_v] = ulp_u;
        }
        else {
            parent[ulp_v] = ulp_u;
            rank[ulp_u]++;
        }
    }

    void unionBySize(int u, int v) {
        int ulp_u = findUPar(u);
        int ulp_v = findUPar(v);
        if (ulp_u == ulp_v) return;
        if (size[ulp_u] < size[ulp_v]) {
            parent[ulp_u] = ulp_v;
            size[ulp_v] += size[ulp_u];
        }
        else {
            parent[ulp_v] = ulp_u;
            size[ulp_u] += size[ulp_v];
        }
    }
};

class Solution
{
	public:
	//Function to find sum of weights of edges of the Minimum Spanning Tree.
    int spanningTree(int V, vector<vector<int>> adj[])
    {
        vector<pair<int, pair<int, int>>> edges;
        for (int i = 0; i < V; i++) {
            for (auto it : adj[i]) {
                int adjNode = it[0];
                int wt = it[1];
                int node = i;

                edges.push_back({wt, {node, adjNode}});
            }
        }
        DisjointSet ds(V);
        sort(edges.begin(), edges.end());
        int mstWt = 0;
        for (auto it : edges) {
            int wt = it.first;
            int u = it.second.first;
            int v = it.second.second;

            if (ds.findUPar(u) != ds.findUPar(v)) {
                mstWt += wt;
                ds.unionBySize(u, v);
            }
        }

        return mstWt;
    }
};
```

