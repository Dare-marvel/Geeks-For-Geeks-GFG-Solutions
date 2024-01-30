### [Replace O's with X's](https://www.geeksforgeeks.org/problems/replace-os-with-xs0052/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=replace-os-with-xs)

## [Explanation](https://takeuforward.org/graph/surrounded-regions-replace-os-with-xs/)

## Code:
```cpp
// User function Template for C++
class Solution{
public:
    // Depth-First Search (DFS) function to traverse and mark 'O' connected components as visited
    void dfs(int row, int col, vector<vector<char>> &mat, vector<vector<int>> &vis, int n, int m) {
        // Define the possible directions to move: up, right, down, left
        int delrow[] = {-1, 0, 1, 0};
        int delcol[] = {0, 1, 0, -1};

        // Mark the current cell as visited
        vis[row][col] = 1;

        // Explore all four directions from the current cell
        for (int i = 0; i < 4; i++) {
            int nrow = row + delrow[i];
            int ncol = col + delcol[i];

            // Check if the new position is within the boundaries and is an unvisited 'O'
            if (nrow >= 0 && nrow < n && ncol >= 0 && ncol < m && !vis[nrow][ncol] && mat[nrow][ncol] == 'O') {
                // Recursive call to explore the connected component
                dfs(nrow, ncol, mat, vis, n, m);
            }
        }   
    }

    // Main function to fill surrounded 'O's with 'X'
    vector<vector<char>> fill(int n, int m, vector<vector<char>> mat) {
        // Create a matrix to keep track of visited cells
        vector<vector<int>> vis(n, vector<int>(m, 0));

        // Traverse and mark connected components starting from the first and last rows
        for (int i = 0; i < m; i++) {
            // First row
            if (!vis[0][i] && mat[0][i] == 'O') {
                dfs(0, i, mat, vis, n, m);
            }

            // Last row
            if (!vis[n-1][i] && mat[n-1][i] == 'O') {
                dfs(n-1, i, mat, vis, n, m);
            }
        }

        // Traverse and mark connected components starting from the first and last columns
        for (int j = 0; j < n; j++) {
            // First column
            if (!vis[j][0] && mat[j][0] == 'O') {
                dfs(j, 0, mat, vis, n, m);
            }

            // Last column
            if (!vis[j][m-1] && mat[j][m-1] == 'O') {
                dfs(j, m-1, mat, vis, n, m);
            }
        }

        // Replace unvisited 'O's with 'X'
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (!vis[i][j] && mat[i][j] == 'O') {
                    mat[i][j] = 'X';
                }
            }
        }

        // Return the modified matrix
        return mat;
    }
};
```
