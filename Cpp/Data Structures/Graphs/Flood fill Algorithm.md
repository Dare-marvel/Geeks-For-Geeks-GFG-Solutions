### [Flood fill Algorithm](https://www.geeksforgeeks.org/problems/flood-fill-algorithm1856/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=flood-fill-algorithm)

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Code:
```cpp
// Definition of a class named Solution
class Solution {
public:
    // Depth-First Search (DFS) function to perform flood fill starting from a given cell
    void dfs(int row, int col, vector<vector<int>>& ans, vector<vector<int>>& image, int newColor, int iniColor) {
        // Array to represent the changes in row and column for exploring neighboring cells
        int delrow[] = {-1, 0, 1, 0};
        int delcol[] = {0, 1, 0, -1};

        // Set the new color for the current cell
        ans[row][col] = newColor;

        // Get the dimensions of the image
        int n = image.size();
        int m = image[0].size();

        // Iterate through the neighboring cells
        for (int i = 0; i < 4; i++) {
            int nrow = row + delrow[i];
            int ncol = col + delcol[i];

            // Check if the neighboring cell is within the boundaries and has the initial color
            if (nrow >= 0 && nrow < n && ncol >= 0 && ncol < m && image[nrow][ncol] == iniColor && ans[nrow][ncol] != newColor) {
                // Perform DFS for the neighboring cell
                dfs(nrow, ncol, ans, image, newColor, iniColor);
            }
        } 
    }

    // Function to perform flood fill on the given image
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int newColor) {
        // Store the initial color of the starting cell
        int iniColor = image[sr][sc];

        // Assign a reference to the original image to the answer variable
        vector<vector<int>>& ans = image;

        // Perform DFS to flood fill the image
        dfs(sr, sc, ans, image, newColor, iniColor);

        // Return the flooded image
        return ans;
    }
};

```
