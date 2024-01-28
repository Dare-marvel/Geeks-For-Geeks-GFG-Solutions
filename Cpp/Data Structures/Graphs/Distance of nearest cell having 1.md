### [Distance of nearest cell having 1](https://www.geeksforgeeks.org/problems/distance-of-nearest-cell-having-1-1587115620/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=distance-of-nearest-cell-having-1)

## [Explanation](https://takeuforward.org/graph/distance-of-nearest-cell-having-1/)

## Code:
```cpp
class Solution 
{
public:
    // Function to find distance of nearest 1 in the grid for each cell.
    vector<vector<int>> nearest(vector<vector<int>> grid)
    {
        // Get the number of rows and columns in the grid.
        int n = grid.size();
        int m = grid[0].size();
        
        // Initialize a matrix to track visited cells.
        vector<vector<int>> vis(n, vector<int>(m, 0));
        
        // Initialize a matrix to store distances from each cell to the nearest 1.
        vector<vector<int>> dist(n, vector<int>(m, 0));
        
        // Initialize a queue for BFS traversal.
        queue<pair<pair<int, int>, int>> q;
        
        // Push all cells with '1' into the queue and mark them as visited.
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (grid[i][j] == 1) {
                    q.push({{i, j}, 0});
                    vis[i][j] = 1;
                }
            }
        }
        
        // Arrays to represent possible movements - up, right, down, left.
        int delrow[] = {-1, 0, 1, 0};
        int delcol[] = {0, 1, 0, -1};
        
        // Perform BFS traversal.
        while (!q.empty()) {
            int row = q.front().first.first;
            int col = q.front().first.second;
            int steps = q.front().second;
            
            // Store the distance in the 'dist' matrix and dequeue the current cell.
            dist[row][col] = steps;
            q.pop();
            
            // Check adjacent cells and enqueue them if not visited.
            for (int i = 0; i < 4; i++) {
                int nrow = row + delrow[i];
                int ncol = col + delcol[i];
                
                // Ensure the cell is within the grid boundaries and has not been visited.
                if (nrow >= 0 && nrow < n && ncol >= 0 && ncol < m && vis[nrow][ncol] == 0) {
                    // Mark the cell as visited and enqueue it with updated steps.
                    vis[nrow][ncol] = 1;
                    q.push({{nrow, ncol}, steps + 1});
                }
            }
        }
        
        // Return the matrix containing distances to the nearest '1'.
        return dist;
    }
};

```
