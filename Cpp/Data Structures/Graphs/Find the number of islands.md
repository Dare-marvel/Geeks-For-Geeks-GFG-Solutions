### [Find the number of islands](https://www.geeksforgeeks.org/problems/find-the-number-of-islands/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=find_the_number_of_islands)

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Code:
```cpp
// Definition of a class named Solution
class Solution {
public:
    // Breadth-First Search (BFS) function to explore the island starting from a given cell
    void bfs(int row, int col, vector<vector<int>> &vis, vector<vector<char>>& grid) {
        int n = grid.size();
        int m = grid[0].size();

        // Mark the current cell as visited
        vis[row][col] = 1;
        
        // Create a queue to perform BFS
        queue<pair<int, int>> q;
        q.push({row, col});

        // Perform BFS to explore the entire island
        while (!q.empty()) {
            int crow = q.front().first;
            int ccol = q.front().second;
            q.pop();

            // Explore adjacent cells
            for (int delrow = -1; delrow <= 1; delrow++) {
                for (int delcol = -1; delcol <= 1; delcol++) {
                    int nrow = crow + delrow;
                    int ncol = ccol + delcol;

                    // Check if the adjacent cell is within the grid boundaries and is not visited
                    // Also, the cell should contain '1' indicating land
                    if (nrow >= 0 && nrow < n && ncol >= 0 && ncol < m && !vis[nrow][ncol] && grid[nrow][ncol] == '1') {
                        // Mark the adjacent cell as visited and enqueue it
                        vis[nrow][ncol] = 1;
                        q.push({nrow, ncol});
                    }
                }
            }
        }
    }

    // Function to find the number of islands in the given grid
    int numIslands(vector<vector<char>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        int count = 0;

        // 2D array to mark visited cells
        vector<vector<int>> vis(n, vector<int>(m, 0));

        // Iterate through each cell in the grid
        for (int row = 0; row < n; row++) {
            for (int col = 0; col < m; col++) {
                // If the cell is unvisited and contains '1' (land), start exploring the island
                if (!vis[row][col] && grid[row][col] == '1') {
                    count++; // Increment the island count
                    bfs(row, col, vis, grid); // Perform BFS to explore the island
                }
            }
        }

        // Return the total count of islands
        return count;
    }
};
```
