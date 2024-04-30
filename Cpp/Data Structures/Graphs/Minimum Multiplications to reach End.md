### [Minimum Multiplications to reach End](https://www.geeksforgeeks.org/problems/minimum-multiplications-to-reach-end/1)

## **Approach and Intuition:**:
1. **Problem Description**: The problem aims to find the minimum number of multiplications required to transform a given number `start` into another number `end`, using a set of integers provided in the vector `arr`.

2. **Breadth-First Search (BFS)**: The code utilizes a BFS approach to explore all possible transformations from the starting number to the target number. BFS is a suitable choice for this problem as it guarantees finding the shortest path to the target node.

3. **Queue Initialization**: A queue of pairs `(int, int)` is used to store nodes and their corresponding steps. Each pair represents a node and the number of steps taken to reach that node from the starting point.

4. **Distance Initialization**: A vector `dist` is initialized to store the minimum distance (number of steps) required to reach each node. It is initialized with a large value for all nodes except the starting node, which is set to 0.

5. **Main Loop**: The BFS loop continues until the queue is empty. At each iteration, a node and its corresponding steps are extracted from the front of the queue.

6. **Goal Check**: If the current node matches the target node (`end`), the function returns the number of steps taken to reach it. This represents the minimum number of multiplications required.

7. **Multiplication and Modulo Operation**: For each node, the code iterates through each integer in the `arr` vector. It multiplies the current integer with the node value and takes modulo `mod`. This operation simulates the multiplication and ensures the result remains within a certain range.

8. **Updating Distances**: If the number of steps to reach the new node (`num`) is less than the current distance stored in `dist`, the distance is updated with the new number of steps, and the new node is added to the queue with the incremented steps.

9. **Termination**: If the target node cannot be reached from the starting node, the function returns -1, indicating that there is no valid transformation path.

## Time and Space Complexity:
### `Time Complexity`:
- Each node is processed exactly once in the BFS traversal, and for each node, we iterate through each integer in the `arr` vector.
- Therefore, the time complexity is O(N * M), where N is the number of elements in the `arr` vector and M is the maximum value possible for `num` after the modulo operation.
 
### `Space Complexity`:
- The space complexity is O(N + M), where N is the size of the `dist` vector (100000) and M is the size of the queue at its peak, which can be up to the size of the input vector `arr`.

## Code:
```cpp
// Define a class named Solution
class Solution {
  public:
    // Define a function named minimumMultiplications that takes a vector of integers 'arr',
    // and two integers 'start' and 'end' as parameters, and returns an integer
    int minimumMultiplications(vector<int>& arr, int start, int end) {
        // Create a queue of pairs of integers to store nodes and their corresponding steps
        queue<pair<int,int>> q;
        // Initialize the queue with the starting node and 0 steps
        q.push({start,0});
        
        // Create a vector 'dist' to store distances (number of steps) for each node
        vector<int> dist(100000,1e9); // Initialize all distances to a large value
        dist[start] = 0; // Set the distance of the starting node to 0
        int mod = 100000; // Set the modulo value
        
        // Loop until the queue is empty
        while(!q.empty()){
            // Extract the node and its steps from the front of the queue
            int node = q.front().first;
            int steps = q.front().second;
            q.pop(); // Remove the node from the queue
            
            // If the current node is the destination node, return the number of steps
            if(node == end) return steps;
            
            // Iterate through each integer in the array 'arr'
            for(auto it:arr){
                // Calculate the new number by multiplying the current integer with the node and taking modulo
                int num = (it * node) % mod;
                
                // If the number of steps to reach 'num' is less than the current distance,
                // update the distance and add 'num' to the queue with the incremented steps
                if(steps+1 < dist[num]){
                    dist[num] = steps+1;
                    q.push({num,steps+1});
                }
            }
        }
        
        // If the destination node cannot be reached, return -1
        return -1;
    }
};
```
