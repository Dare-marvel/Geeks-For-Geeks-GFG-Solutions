### [Shortest Distance in a Binary Maze](https://www.geeksforgeeks.org/problems/shortest-path-in-a-binary-maze-1655453161/1)

## Approach and Intuition::
1. **Initialization**:
   - The code starts by checking if the source and destination points are the same. If they are, the shortest distance is obviously 0, so it returns 0.
   - It initializes a queue for BFS traversal, along with a 2D vector to store distances initialized to infinity (1e9).
   - It sets the distance of the source point to 0 and pushes it into the queue to start the traversal.

2. **BFS Traversal**:
   - The code utilizes a queue to perform a BFS traversal of the grid.
   - It explores the grid cells starting from the source point, moving in four directions: up, down, left, and right.
   - For each cell visited, it checks if the new position is within the grid bounds and whether it's reachable (grid[newr][newc] == 1).
   - It also checks if the new distance to the cell is shorter than the previously recorded distance. If so, it updates the distance.
   - If the destination point is reached during traversal, it returns the distance to the destination point.

3. **Shortest Path Determination**:
   - During traversal, the code maintains the shortest distance to each reachable cell from the source point.
   - If the destination point is reached, the code returns the distance to the destination point, which represents the shortest path length.

4. **Handling Unreachable Destination**:
   - If the destination point is not reachable from the source point, the code returns -1 to indicate that there is no valid path.

## Time and Space Complexity:
### `Time Complexity`:
- The time complexity of the provided code is O(n * m), where n is the number of rows and m is the number of columns in the grid. This complexity arises from the BFS traversal, where each cell in the grid is potentially visited once.

### `Space Complexity`:
- The space complexity of the provided code is O(n * m), where n is the number of rows and m is the number of columns in the grid. This complexity arises from the storage of distances in the 2D vector. Additionally, the queue and other variables consume constant space that is not dependent on the grid size.

## Code:
```cpp
class Solution {
public:
    int shortestPath(vector<vector<int>> &grid, pair<int, int> source,
                     pair<int, int> destination) {
        // Base case: If source and destination are the same, return 0
        if (source.first == destination.first && source.second == destination.second) 
            return 0;
        
        // Initialize a queue for BFS traversal
        queue<pair<int,pair<int,int>>> q;
        
        // Get the number of rows and columns in the grid
        int n = grid.size();
        int m = grid[0].size();
        
        // Initialize a 2D vector to store distances, initially set to infinity
        vector<vector<int>> dist(n, vector<int>(m, 1e9));
        dist[source.first][source.second] = 0; // Set distance of source to 0
        
        // Push source node into the queue along with its distance
        q.push({0, {source.first, source.second}});
        
        // Define directions: up, right, down, left
        int dr[] = {-1, 0, 1, 0};
        int dc[] = {0, 1, 0, -1};

        // BFS traversal
        while (!q.empty()) {
            auto it = q.front(); // Get the front element of the queue
            
            q.pop(); // Remove the front element from the queue
            int dis = it.first; // Current distance
            int r = it.second.first; // Current row
            int c = it.second.second; // Current column
            
            // Explore all four directions
            for (int i = 0; i < 4; i++) {
                int newr = r + dr[i]; // New row
                int newc = c + dc[i]; // New column
                
                // Check if the new position is within the grid bounds and is reachable (grid[newr][newc] == 1)
                // Also, check if the new distance is shorter than the previously recorded distance
                if (newr >= 0 && newr < n && newc >= 0 && newc < m && grid[newr][newc] == 1 && 
                    (1 + dis < dist[newr][newc])) {
                    
                    // Update the distance for the new position
                    dist[newr][newc] = 1 + dis;
                    
                    // If the destination is reached, return the distance
                    if (newr == destination.first && newc == destination.second) {
                        return dis + 1;
                    }
                    
                    // Push the new position into the queue along with its updated distance
                    q.push({dis + 1, {newr, newc}});
                }
            }
        }
        
        // If the destination is not reachable, return -1
        return -1;
    }
};
```
