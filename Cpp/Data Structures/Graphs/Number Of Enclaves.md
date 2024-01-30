### [Number Of Enclaves](https://www.geeksforgeeks.org/problems/number-of-enclaves/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=number-of-enclaves)

## [Explanation](https://takeuforward.org/graph/number-of-enclaves/)

## Code:
```cpp
class Solution {
  public:
    // Function to calculate the number of enclaves
    int numberOfEnclaves(vector<vector<int>> &grid) {
        // Code here

        // Initialize a queue to perform BFS
        queue<pair<int, int>> q; 

        // Get the dimensions of the grid
        int n = grid.size(); 
        int m = grid[0].size(); 

        // Create a 2D array to keep track of visited cells
        int vis[n][m] = {0}; 

        // Traverse boundary elements
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                // Check if it's on the boundary
                if(i == 0 || j == 0 || i == n-1 || j == m-1) {
                    // If it's land, store it in the queue and mark as visited
                    if(grid[i][j] == 1) {
                        q.push({i, j}); 
                        vis[i][j] = 1; 
                    }
                }
            }
        }
        
        // Define directions to move: up, right, down, left
        int delrow[] = {-1, 0, +1, 0};
        int delcol[] = {0, +1, +0, -1}; 

        // Perform BFS
        while(!q.empty()){
            int row = q.front().first;
            int col = q.front().second;
            
            q.pop();
            
            // Explore neighbors
            for(int i = 0; i < 4; i++){
                int nrow = row + delrow[i];
                int ncol = col + delcol[i];
                
                // Check if the neighbor is within bounds, unvisited, and is land
                if(nrow >= 0 && nrow < n && ncol >= 0 && ncol < m 
                && !vis[nrow][ncol] && grid[nrow][ncol] == 1){
                    // Mark as visited and add to the queue
                    vis[nrow][ncol] = 1;
                    q.push({nrow, ncol});
                }
            }
        }
        
        // Count unvisited land cells
        int cnt = 0;
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                // Check for unvisited land cell
                if(grid[i][j] == 1 && vis[i][j] == 0) 
                    cnt++; 
            }
        }
        // Return the count of enclaves
        return cnt; 
    }
};

```
