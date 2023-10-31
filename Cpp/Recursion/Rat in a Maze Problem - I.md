### [Rat in a Maze Problem - I](https://practice.geeksforgeeks.org/problems/rat-in-a-maze-problem/1)

## Explanation:
This C++ code is a solution for finding all possible paths from the top-left cell to the bottom-right cell in a given 2D grid. The grid is represented as a 2D array where 1 indicates a valid cell to move to and 0 indicates a blocked cell. Here's a detailed explanation of the main logic:

1. **Class Definition**: The `Solution` class is defined with two methods: `findPath` and `findPathHelper`.

2. **Public Method - findPath**: This is the public method that takes an input 2D vector of integers (`m`) and an integer (`n`) representing the size of the grid. It initializes an empty vector (`ans`) to store the paths and a 2D vector (`vis`) to keep track of visited cells. If the top-left cell is valid (i.e., `m[0][0]` is 1), it calls the helper method `findPathHelper` to fill `ans`. It then returns `ans`.

3. **Private Method - findPathHelper**: This is a private helper method that finds paths recursively. It takes several parameters: the current cell (`i`, `j`), the grid (`a`), the size of the grid (`n`), the vector to store all paths (`ans`), the current path (`move`), and the visited matrix (`vis`).

4. **Base Case**: In `findPathHelper`, if `i` and `j` are both equal to `n-1`, it means we have reached the bottom-right cell, so we add `move` to `ans` and return.

5. **Recursive Case**: If we haven't reached the bottom-right cell, we try moving in all four directions (down, left, right, up) from the current cell. For each direction, if moving in that direction leads to a valid and unvisited cell, we mark the current cell as visited, append the direction to `move`, make a recursive call with the new cell, and then mark the current cell as unvisited. This backtracking ensures that all paths are found.
  
## Time and Space Complexity:
### `Time Complexity`:
The time complexity is O(4^(n*m)) because in worst case scenario, from each cell we have 4 options to choose and we have total n*m cells.

### `Space Complexity`:
The space complexity is O(n*m) because in worst case scenario depth of recursion tree can go upto n*m.

## Code:
```cpp
// Function to find paths in a 2D grid from top-left to bottom-right
void findPathHelper(int i, int j, vector<vector<int>>& a, int n, vector<string>& ans, string move,
                    vector<vector<int>>& vis) {
    // Base case: If the current position is the bottom-right corner of the grid
    if (i == n - 1 && j == n - 1) {
        // Add the current path to the answer vector
        ans.push_back(move);
        return;
    }

    // Explore possible moves: downward, left, right, upward

    // Downward move
    if (i + 1 < n && !vis[i + 1][j] && a[i + 1][j] == 1) {
        // Mark the current cell as visited
        vis[i][j] = 1;
        // Recur with the downward move and update the path string
        findPathHelper(i + 1, j, a, n, ans, move + 'D', vis);
        // Backtrack: mark the current cell as unvisited
        vis[i][j] = 0;
    }

    // Left move
    if (j - 1 >= 0 && !vis[i][j - 1] && a[i][j - 1] == 1) {
        vis[i][j] = 1;
        findPathHelper(i, j - 1, a, n, ans, move + 'L', vis);
        vis[i][j] = 0;
    }

    // Right move
    if (j + 1 < n && !vis[i][j + 1] && a[i][j + 1] == 1) {
        vis[i][j] = 1;
        findPathHelper(i, j + 1, a, n, ans, move + 'R', vis);
        vis[i][j] = 0;
    }

    // Upward move
    if (i - 1 >= 0 && !vis[i - 1][j] && a[i - 1][j] == 1) {
        vis[i][j] = 1;
        findPathHelper(i - 1, j, a, n, ans, move + 'U', vis);
        vis[i][j] = 0;
    }
}

// Public function to initiate the path finding process
public:
    vector<string> findPath(vector<vector<int>>& m, int n) {
        // Vector to store the resulting paths
        vector<string> ans;
        // 2D vector to track visited cells
        vector<vector<int>> vis(n, vector<int>(n, 0));
        // Check if the top-left corner is a valid starting point
        if (m[0][0] == 1) 
            // Call the helper function starting from the top-left corner
            findPathHelper(0, 0, m, n, ans, "", vis);
        // Return the vector containing all possible paths
        return ans;
    }
};
```
