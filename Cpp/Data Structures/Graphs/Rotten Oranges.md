### [Rotten Oranges](https://www.geeksforgeeks.org/problems/rotten-oranges2536/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=rotten_oranges)

## [Explanation](https://takeuforward.org/data-structure/rotten-oranges/)

## Code:
```cpp
// Definition of a class named Solution
class Solution {
public:
    // Function to find the minimum time required to rot all oranges
    int orangesRotting(vector<vector<int>>& grid) {
        // Get the dimensions of the grid
        int n = grid.size();
        int m = grid[0].size();

        // 2D vector to track the state of oranges (0: unvisited, 1: fresh orange, 2: rotten orange)
        vector<vector<int>> vis(n, vector<int>(m, 0));

        // Queue to perform Breadth-First Search (BFS) for rotting oranges
        queue<pair<pair<int, int>, int>> q;

        // Count the number of fresh oranges
        int cntFresh = 0;

        // Initialize the queue with rotten oranges and mark them as visited
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (grid[i][j] == 2) {
                    q.push({{i, j}, 0});
                    vis[i][j] = 2;  // Marking a rotten orange
                } else {
                    vis[i][j] = 0;  // Marking an unvisited cell
                }

                if (grid[i][j] == 1) {
                    cntFresh++;  // Counting fresh oranges
                }
            }
        }

        int tm = 0;  // Variable to store the time required for all oranges to rot

        // Arrays to represent changes in row and column for exploring neighboring cells
        int drow[] = {-1, 0, +1, 0};
        int dcol[] = {0, 1, 0, -1};
        int cnt = 0;  // Counter for the number of rotten oranges

        // Perform BFS to find the minimum time required for all oranges to rot
        while (!q.empty()) {
            int r = q.front().first.first;
            int c = q.front().first.second;
            int t = q.front().second;
            tm = max(tm, t);  // Update the time variable
            q.pop();

            // Explore neighboring cells
            for (int i = 0; i < 4; i++) {
                int nrow = r + drow[i];
                int ncol = c + dcol[i];

                // Check if the neighboring cell is within the grid boundaries,
                // contains a fresh orange, and has not been visited
                if (nrow >= 0 && nrow < n && ncol >= 0 && ncol < m && grid[nrow][ncol] == 1 && vis[nrow][ncol] == 0) {
                    q.push({{nrow, ncol}, t + 1});  // Enqueue the neighboring cell with the updated time
                    vis[nrow][ncol] = 2;  // Mark the neighboring cell as rotten
                    cnt++;  // Increment the count of rotten oranges
                }
            }
        }

        // If the count of rotten oranges is not equal to the count of fresh oranges,
        // then not all oranges can be rotten, return -1
        if (cnt != cntFresh) {
            return -1;
        }

        // Return the minimum time required for all oranges to rot
        return tm;
    }
};

```
