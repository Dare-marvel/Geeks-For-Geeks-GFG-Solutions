### [Disjoint Set](https://takeuforward.org/data-structure/disjoint-set-union-by-rank-union-by-size-path-compression-g-46/)

## Approach and Intuition:

1. **Disjoint Set Data Structure**: The code implements a Disjoint Set data structure, which is used to maintain a collection of disjoint sets. It is often employed to solve problems involving connectivity and partitioning of a set.

2. **Initialization**: 
   - The `DisjointSet` class is initialized with a parameter `n`, representing the number of elements in the set.
   - Two vectors, `rank` and `parent`, are created to store the rank and parent of each element, respectively. 
   - Initially, each element is its own parent, and its rank is set to 0.

3. **Find Operation (`findUPar`)**: 
   - The `findUPar` function recursively finds the ultimate parent (representative) of a given element in its disjoint set.
   - It utilizes path compression by updating the parent of each visited node to the ultimate parent, reducing the depth of the tree.

4. **Union Operation (`unionByRank`)**:
   - The `unionByRank` function performs the union operation between two elements by their ultimate parents.
   - It compares the ranks of the two sets and merges them accordingly to ensure efficient union and balanced tree structure.
   - If both sets have the same rank, one set is chosen as the parent, and its rank is incremented.

5. **Main Function (`main`)**:
   - In the `main` function, a `DisjointSet` object `ds` is created with 7 elements.
   - Several union operations are performed between different elements.
   - The code then checks if nodes 3 and 7 belong to the same set before and after performing a union operation between them.
   - The results are printed to indicate whether nodes 3 and 7 are in the same set or not.

## Time and Space Complexity:
### `Time Complexity`:
- **Initialization**: 
  - Time complexity: O(n)
- **Find Operation (`findUPar`)**:
  - Time complexity: O(log n) on average due to path compression.
- **Union Operation (`unionByRank`)**:
  - Time complexity: O(log n) on average due to union by rank.
  
### `Space Complexity`:
- The space complexity of the code is O(n), where n is the number of elements in the disjoint set.

## Code:
```cpp
#include <bits/stdc++.h> // Include standard C++ libraries
using namespace std;

class DisjointSet{ // Define a class for Disjoint Set data structure
    vector<int> rank,parent; // Define vectors for rank and parent nodes
    
public:
    // Constructor to initialize Disjoint Set with 'n' nodes
    DisjointSet(int n){
        rank.resize(n+1,0); // Resize rank vector and initialize with 0
        parent.resize(n+1); // Resize parent vector
        for(int i=0;i<=n;i++){
            parent[i] = i; // Initialize each node's parent as itself
        }
    }
    
    // Function to find the parent of a node using path compression technique
    int findUPar(int node){
        if(node == parent[node]){ // If the node is its own parent
            return node; // Return the node itself
        }
        else return parent[node] = findUPar(parent[node]); // Path compression by updating parent
    }
    
    // Function to perform union operation by rank
    void unionByRank(int u,int v){
        int ulp_u = findUPar(u); // Find parent of 'u'
        int ulp_v = findUPar(v); // Find parent of 'v'
        
        if(ulp_u == ulp_v) return; // If 'u' and 'v' belong to the same set
        
        // Union by rank
        if(rank[ulp_u] < rank[ulp_v]){ // If rank of 'u' is less than rank of 'v'
            parent[ulp_u] = ulp_v; // Set parent of 'u' as parent of 'v'
        }
        else if(rank[ulp_v] < rank[ulp_u]){ // If rank of 'v' is less than rank of 'u'
            parent[ulp_v] = ulp_u; // Set parent of 'v' as parent of 'u'
        }
        else{ // If ranks are equal
            parent[ulp_v] = ulp_u; // Set parent of 'v' as parent of 'u'
            rank[ulp_u]++; // Increase rank of 'u'
        }
    }
};

#include <stdio.h> // Include standard C library for printf function

int main()
{
    DisjointSet ds(7); // Create a Disjoint Set object with 7 nodes
    ds.unionByRank(1, 2); // Union operation between nodes 1 and 2
    ds.unionByRank(2, 3); // Union operation between nodes 2 and 3
    ds.unionByRank(4, 5); // Union operation between nodes 4 and 5
    ds.unionByRank(6, 7); // Union operation between nodes 6 and 7
    ds.unionByRank(5, 6); // Union operation between nodes 5 and 6
    
    // Check if nodes 3 and 7 belong to the same set
    if (ds.findUPar(3) == ds.findUPar(7)) {
        cout << "Same\n"; // Print "Same" if nodes belong to the same set
    }
    else cout << "Not same\n"; // Print "Not same" otherwise

    ds.unionByRank(3, 7); // Union operation between nodes 3 and 7

    // Check again if nodes 3 and 7 belong to the same set
    if (ds.findUPar(3) == ds.findUPar(7)) {
        cout << "Same\n"; // Print "Same" if nodes belong to the same set
    }
    else cout << "Not same\n"; // Print "Not same" otherwise

    return 0; // Return 0 to indicate successful execution
}

```
