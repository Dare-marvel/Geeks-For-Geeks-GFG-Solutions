### [Number of Distinct Islands](https://www.geeksforgeeks.org/problems/number-of-distinct-islands/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=number-of-distinct-islands)

## Explanation:
1. **Purpose**: The code is designed to count the number of distinct islands in a 2D grid. Each island is made up of cells marked with '1' and surrounded by cells marked with '0'. Two islands are considered distinct if they have different shapes or orientations.

2. **DFS Function**: The `dfs` function is a Depth-First Search algorithm used to traverse and collect island coordinates. It starts at a given cell and explores as far as possible along each branch before backtracking.

3. **Visiting Cells**: The `dfs` function marks the current cell as visited and adds its coordinates to a vector. The coordinates are stored relative to the starting point of the island (i.e., `row - row0`, `col - col0`).

4. **Exploring Neighbors**: The function then explores the neighboring cells in four directions: up, left, down, and right. If a neighbor is within bounds, unvisited, and is part of the island (i.e., `grid[nrow][ncol] == 1`), the function makes a recursive call to continue exploring the island.

5. **Counting Islands**: The `countDistinctIslands` function counts the number of distinct islands in the grid. It initializes a 2D vector `vis` to track visited cells and a set `st` to store distinct islands.

6. **Traversing the Grid**: The function traverses the grid cell by cell. If it encounters an unvisited cell that is part of an island, it calls the `dfs` function to collect the island's coordinates.

7. **Storing Islands**: After collecting an island's coordinates, the function inserts the vector of coordinates into the set. The set data structure automatically ignores duplicates, ensuring that only distinct islands are stored.

8. **Returning the Count**: Finally, the function returns the size of the set, which represents the count of distinct islands in the grid.

## Time and Space Complexity:
### `Time Complexity`:
The time complexity of the code is O(N*M), where N and M are the dimensions of the grid. This is because each cell in the grid is visited once by the DFS algorithm.

### `Space Complexity`:
The space complexity is also O(N*M), due to the space required for the `vis` vector and the `vec` vector in the worst case (when all cells are part of the same island).

## Code:
```cpp
class Solution {
  public:
    // Depth-First Search (DFS) function to traverse and collect island coordinates
    void dfs(int row, int col, vector<vector<int>>& vis, vector<vector<int>>& grid, vector<pair<int,int>> &vec, int row0, int col0) {
        int n = grid.size();
        int m = grid[0].size();
        
        // Define possible directions to move: up, left, down, right
        int delrow[] = {-1, 0, 1, 0};
        int delcol[] = {0, -1, 0, 1};
        
        // Mark the current cell as visited and add its coordinates to the vector
        vis[row][col] = 1;
        vec.push_back({row - row0, col - col0});
        
        // Explore neighbors
        for(int i = 0; i < 4; i++) {
            int nrow = row + delrow[i];
            int ncol = col + delcol[i];
            
            // Check if the neighbor is within bounds, unvisited, and is part of the island
            if(nrow >= 0 && nrow < n && ncol >= 0 && ncol < m && !vis[nrow][ncol] && grid[nrow][ncol] == 1) {
                // Recursive call to explore the connected island
                dfs(nrow, ncol, vis, grid, vec, row0, col0);
            }
        }
    }

    // Function to count distinct islands in the given grid
    int countDistinctIslands(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        
        // 2D vector to track visited cells
        vector<vector<int>> vis(n, vector<int>(m, 0));
        // Set to store distinct islands
        set<vector<pair<int, int>>> st;

        // Traverse the grid
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                // If an unvisited cell with an island is found
                if(!vis[i][j] && grid[i][j] == 1) {
                    // Vector to store island coordinates relative to the starting point
                    vector<pair<int, int>> vec;
                    // DFS to collect island coordinates
                    dfs(i, j, vis, grid, vec, i, j);
                    // Insert the vector of coordinates into the set (ignores duplicates)
                    st.insert(vec);
                }
            }
        }
        
        // Return the count of distinct islands
        return st.size();
    }
};

```
