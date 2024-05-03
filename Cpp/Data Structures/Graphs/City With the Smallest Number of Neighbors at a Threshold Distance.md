### [City With the Smallest Number of Neighbors at a Threshold Distance](https://www.geeksforgeeks.org/problems/city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/1)

## Approach:

1. **Initialize Distance Matrix**: 
   - Create a 2D matrix `dist` to represent the distances between cities.
   - Initialize all distances to `INT_MAX` to signify that initially, there's no direct path between any two cities.

2. **Populate Distance Matrix**:
   - Iterate through the list of edges.
   - For each edge, update the corresponding entries in the distance matrix with the edge weight.
   - Since the graph is undirected, update both `dist[it[0]][it[1]]` and `dist[it[1]][it[0]]`.

3. **Set Diagonal Entries to 0**:
   - Set the diagonal entries of the distance matrix to 0, indicating that the distance from a city to itself is 0.

4. **Floyd-Warshall Algorithm**:
   - Use the Floyd-Warshall algorithm to find the shortest paths between all pairs of cities.
   - This algorithm iteratively updates the distance matrix by considering all possible intermediate vertices between any two cities.

5. **Find City with Minimum Reachable Cities**:
   - Initialize variables `cntCity` and `cityNo` to keep track of the city with the minimum number of reachable cities and its index, respectively.
   - Iterate through each city.
   - For each city, count the number of reachable cities within the given distance threshold.
   - Update `cityNo` and `cntCity` if the current city has fewer reachable cities within the threshold.

6. **Return Result**:
   - Return the index of the city with the minimum number of reachable cities.

## Intuition:

- **Initialization**: Initially, we set up a distance matrix representing the distances between all pairs of cities. We set all distances to infinity, except for direct connections between cities, which are populated from the given edge list.

- **Floyd-Warshall Algorithm**: By repeatedly considering all pairs of cities and possible intermediate vertices, the algorithm efficiently finds the shortest paths between all pairs of cities. This is achieved by updating the distance matrix with shorter path lengths whenever a shorter path is found.

- **Counting Reachable Cities**: After computing the shortest paths, we iterate through each city and count the number of cities that can be reached within the given distance threshold. This is done by checking the distances stored in the distance matrix.

- **Selecting Optimal City**: We select the city with the minimum number of reachable cities, ensuring that it's the most centrally located or accessible city within the given distance threshold.

### Time Complexity:
- **Initialization**: O(n^2), where n is the number of cities.
- **Floyd-Warshall Algorithm**: O(n^3), where n is the number of cities.
- **Counting Reachable Cities**: O(n^2), where n is the number of cities.
- **Overall**: O(n^3), dominated by the Floyd-Warshall algorithm.

### Space Complexity:
- **Distance Matrix**: O(n^2), where n is the number of cities, to store the distances between all pairs of cities.
- **Additional Variables**: O(1), for storing counts and indices.
- **Overall**: O(n^2), dominated by the distance matrix.

## Code:
```cpp
class Solution {
public:
    // Function to find the city within the distance threshold
    int findCity(int n, int m, vector<vector<int>>& edges, int distanceThreshold) {
        
        // Initialize a 2D vector to store distances between cities, initialized with maximum value
        vector<vector<int>> dist(n,vector<int>(n,INT_MAX));
        
        // Populate the distance matrix with edge weights
        for(auto it: edges){
            dist[it[0]][it[1]] = it[2];
            dist[it[1]][it[0]] = it[2];
        }
        
        // Set the diagonal of the distance matrix to 0
        for(int i=0;i<n;i++) dist[i][i] = 0;
        
        // Floyd-Warshall algorithm to find shortest paths between all pairs of cities
        for(int k=0;k<n;k++){
            for(int i=0;i<n;i++){
                for(int j=0;j<n;j++){
                    if(dist[i][k] == INT_MAX || dist[k][j] == INT_MAX){
                        continue;
                    }
                    dist[i][j] = min(dist[i][j],dist[i][k]+dist[k][j]);
                }
            }
        }
        
        // Initialize variables to track the city with the minimum number of reachable cities within distanceThreshold
        int cntCity = n;
        int cityNo = -1;
        int cnt = 0;
        
        // Iterate over each city to find the one with the minimum number of reachable cities within distanceThreshold
        for(int city = 0; city < n; city++){
            cnt = 0;
            
            // Count the number of reachable cities from the current city within distanceThreshold
            for(int adjCity = 0; adjCity < n; adjCity++){
                if(dist[city][adjCity] <= distanceThreshold){
                    cnt++;
                }
            }
            
            // Update the cityNo and cntCity if the current city has fewer reachable cities within distanceThreshold
            if(cnt <= cntCity){
                cityNo = city;
                cntCity = cnt;
            }
        }
        
        // Return the city with the minimum number of reachable cities within distanceThreshold
        return cityNo;
    }
};
```
