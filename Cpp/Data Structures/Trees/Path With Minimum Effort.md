### [Path With Minimum Effort](https://www.geeksforgeeks.org/problems/path-with-minimum-effort/1)

## **Approach and Intuition:**

1. **Problem Understanding:**
   - We're given a grid representing different heights.
   - We need to find the minimum effort required to move from the top-left cell to the bottom-right cell.
   - Effort is defined as the maximum absolute difference in heights between adjacent cells along the path.

2. **Priority Queue for Dijkstra's Algorithm:**
   - We'll use Dijkstra's algorithm to find the shortest path.
   - Priority queue helps select cells with the minimum effort first.

3. **Initialization:**
   - Initialize a priority queue to store cells based on effort.
   - Initialize a 2D array 'dist' to store the minimum effort to reach each cell. Set all values to a large number.
   - Start from the top-left cell with zero effort and push it into the priority queue.

4. **Movement and Exploration:**
   - Define arrays 'dr' and 'dc' for possible movements: up, right, down, left.
   - While the priority queue is not empty, pop the cell with the minimum effort.
   - Explore all possible adjacent cells.
   - Calculate the new effort required to reach each adjacent cell.
   - If the new effort is less than the recorded effort for that cell, update the effort and push it into the priority queue.

5. **Termination:**
   - When the destination cell (bottom-right) is reached, return the effort recorded for that cell.

## Time and Space Complexity:
### `Time Complexity`:
- The time complexity is O(R * C * log(R * C)), where R is the number of rows and C is the number of columns in the grid. 
- Each cell can be pushed into the priority queue at most once, and each operation on the priority queue takes log(R * C) time.

### `Space Complexity`:
- The space complexity is O(R * C) for the 'dist' array and the priority queue.
- 'dist' array stores effort for each cell, and the priority queue stores cell coordinates and their associated efforts.

## Code:
```cpp
class Solution {
  public:
    // Function to calculate the minimum effort required to traverse the heights
    int MinimumEffort(int rows, int columns, vector<vector<int>> &heights) {
        
        // Priority queue to store the difference in heights and the corresponding cell coordinates
        // The queue is sorted in ascending order of the difference in heights
        priority_queue<pair<int,pair<int,int>>, 
        vector<pair<int,pair<int,int>>>,
        greater<pair<int,pair<int,int>>>
        >
        pq;
        
        // Number of rows in the heights matrix
        int n = heights.size();
        
        // Number of columns in the heights matrix
        int m = heights[0].size();
        
        // Matrix to store the minimum effort required to reach each cell from the starting cell
        // Initially, the effort for all cells is set to a large value
        vector<vector<int>> dist(n,vector<int>(m,1e9));
        
        // The effort required to reach the starting cell is 0
        dist[0][0] = 0;
        
        // Add the starting cell to the priority queue
        pq.push({0,{0,0}});
        
        // Arrays to store the possible directions of movement from a cell
        int dr[] = {-1, 0, 1, 0};
        int dc[] = {0, 1, 0, -1};
        
        // Loop until the priority queue is empty
        while(!pq.empty()){
            // Get the cell with the minimum effort from the priority queue
            auto it = pq.top();
            
            // Remove the cell from the priority queue
            pq.pop();
            
            // The effort required to reach the current cell
            int diff = it.first;
            // The coordinates of the current cell
            int row = it.second.first;
            int col = it.second.second;
            
            // If the current cell is the destination cell, return the effort
            if(row == n-1 && col == m-1) return diff;
            
            // Loop through all possible directions of movement
            for(int i=0;i<4;i++){
                // Calculate the coordinates of the new cell
                int newr = row + dr[i];
                int newc = col + dc[i];
                
                // If the new cell is within the heights matrix
                if(newr >= 0 && newr < n && newc >= 0 && newc < m){
                    // Calculate the effort required to reach the new cell
                    int newEffort = max(abs(heights[newr][newc] - heights[row][col]), diff);
                    
                    // If the new effort is less than the current effort for the new cell
                    if(newEffort < dist[newr][newc]){
                        // Update the effort for the new cell
                        dist[newr][newc] = newEffort;
                        // Add the new cell to the priority queue
                        pq.push({newEffort,{newr,newc}});
                    }
                }
            }
        }
        // If the destination cell is not reachable, return 0
        return 0;
    }
};
```
