### [Find the number of islands](https://www.geeksforgeeks.org/problems/find-the-number-of-islands/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=find_the_number_of_islands)

## Explanation:
1. **Class Definition**: The code is encapsulated within a class named `Solution`. This is a common practice in C++ to organize related functions and data together.

2. **BFS Function**: Inside the class, there's a public function `bfs` which takes four parameters: two integers `row` and `col` representing the current cell, a 2D vector `vis` to keep track of visited cells, and a 2D vector `grid` representing the grid of cells.

3. **BFS Algorithm**: The BFS algorithm starts by marking the current cell as visited (`vis[row][col] = 1`) and pushing it into a queue `q`. Then, it enters a while loop that continues until the queue is empty. Inside the loop, it pops the front cell from the queue and checks its neighboring cells. If a neighboring cell is within the grid, has not been visited, and is a land cell (i.e., `grid[nrow][ncol] == '1'`), it marks the cell as visited and pushes it into the queue.

4. **Number of Islands Function**: There's another public function `numIslands` which takes a 2D vector `grid` representing the grid of cells. This function calculates the number of islands (or connected components of land cells) in the grid.

5. **Visited Array Initialization**: The function first initializes the 2D visited array `vis` to `0`.

6. **Count Initialization**: The function also initializes a counter `count` to `0`. This counter keeps track of the number of islands.

7. **BFS Traversal**: The function then starts a BFS traversal from each land cell `grid[row][col] == '1'` that has not been visited. For each such cell, it increments the counter `count` and calls the `bfs` function.

8. **Return Statement**: Finally, the function `numIslands` returns the counter `count`, which is the number of islands in the grid.

## Time and Space Complexity:
### `Time Complexity`:
The **time complexity** of this code is **O(n*m)**, where `n` is the number of rows and `m` is the number of columns in the grid. This is because each cell in the grid is visited at most once.

### `Space Complexity`:
The **space complexity** of this code is **O(n*m)**, due to the space required for the visited array and the queue in the worst case.

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
