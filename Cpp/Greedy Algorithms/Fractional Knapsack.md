### [Fractional Knapsack](https://www.geeksforgeeks.org/problems/fractional-knapsack-1587115620/1)

## Explanation:
### Problem Understanding

**Fractional Knapsack Problem**:
- You have a knapsack with a weight capacity `w`.
- You have `n` items, each with a value (`value`) and a weight (`weight`).
- You can take fractions of items to maximize the total value in the knapsack.

### Approach and Intuition

The primary goal is to maximize the total value that can be accommodated in the knapsack. This can be achieved using a **greedy algorithm** by always choosing the item with the highest value-to-weight ratio first.

### Steps in the Code

1. **Struct Definition**:
   ```cpp
   struct Item{
       int value;
       int weight;
   };
   ```
   This struct represents an item with its `value` and `weight`.

2. **Function Definition**:
   ```cpp
   class Solution {
     public:
       double fractionalKnapsack(int w, Item arr[], int n) {
           std::priority_queue<std::pair<double, int>> pq;
           double totalValue = 0.0;
   ```
   - The function `fractionalKnapsack` takes the maximum weight `w`, an array of items `arr`, and the number of items `n`.
   - A **priority queue** (`pq`) is used to store the items based on their value-to-weight ratio in descending order.
   - `totalValue` keeps track of the total value accumulated in the knapsack.

3. **Calculating Value-to-Weight Ratios**:
   ```cpp
   for(int i = 0; i < n; i++){
       double ratio = (double)arr[i].value / arr[i].weight;
       pq.push({ratio, i});
   }
   ```
   - For each item, calculate its value-to-weight ratio using `(double)arr[i].value / arr[i].weight`.
   - Push each item into the priority queue as a pair of its ratio and its index.

4. **Processing the Items**:
   ```cpp
   int remWt = w;
   while(remWt > 0 && !pq.empty()){
       auto it = pq.top();
       pq.pop();
       int index = it.second;
       double ratio = it.first;
   ```
   - `remWt` is initialized to the remaining capacity of the knapsack, starting with `w`.
   - Use a **while loop** to process items from the priority queue until the knapsack is full (`remWt` becomes 0) or the queue is empty.
   - `it` is the item with the highest value-to-weight ratio (top of the priority queue). Extract it using `pq.top()` and then remove it from the queue with `pq.pop()`.
   - Extract the item's index and ratio.

5. **Taking Items into the Knapsack**:
   ```cpp
   if(remWt >= arr[index].weight){
       totalValue += arr[index].value;
       remWt -= arr[index].weight;
   }
   else {
       totalValue += remWt * ratio;
       remWt = 0;
   }
   ```
   - If the remaining weight (`remWt`) is greater than or equal to the item's weight, take the entire item:
     - Add its value to `totalValue`.
     - Subtract its weight from `remWt`.
   - If the remaining weight is less than the item's weight, take a fraction of the item:
     - Add the fraction of its value that fits into the remaining weight (`remWt * ratio`) to `totalValue`.
     - Set `remWt` to 0 as the knapsack is now full.

6. **Return the Total Value**:
   ```cpp
   return totalValue;
   ```
   - Finally, return the total value accumulated in the knapsack.

## Time and Space Complexity

### **Time Complexity**:
- **Sorting and Priority Queue Operations**: Inserting `n` items into the priority queue takes (O(n log n)) time.
- **Processing Items**: Extracting items from the priority queue also takes (O(n log n)) in the worst case.
- **Overall**: The dominant factor is the priority queue operations, resulting in an overall time complexity of (O(n log n)).

### **Space Complexity**:
- **Auxiliary Space**: The priority queue itself consumes \(O(n)\) space.
- **Overall**: The space complexity is \(O(n)\), mainly due to the storage requirements of the priority queue.

### Summary

- **Key Concept**: The algorithm uses a **greedy approach**, prioritizing items based on their value-to-weight ratio.
- **Efficiency**: The use of a **priority queue** ensures efficient extraction of the next best item.
- **Flexibility**: By handling fractional items, the algorithm maximizes the total value within the given weight constraint.

This approach ensures that the maximum possible value is obtained in the knapsack, leveraging the power of the priority queue for optimal selection.

## Code:
```cpp
// Struct to represent an item with a value and weight
/*
struct Item{
    int value;
    int weight;
};
*/

class Solution {
  public:
    // Function to get the maximum total value in the knapsack.
    double fractionalKnapsack(int w, Item arr[], int n) {
        // Priority queue to store value-to-weight ratios in descending order
        std::priority_queue<std::pair<double, int>> pq;
        double totalValue = 0.0; // Variable to store the total value of items in the knapsack
        
        // Calculate value-to-weight ratios and push them into the priority queue
        for(int i = 0; i < n; i++){
            double ratio = (double)arr[i].value / arr[i].weight; // Calculate value-to-weight ratio
            pq.push({ratio, i}); // Push the ratio and item index into the priority queue
        }
        
        int remWt = w; // Variable to store the remaining weight capacity of the knapsack
        
        // Process the items in the order of their value-to-weight ratios
        while(remWt > 0 && !pq.empty()){
            auto it = pq.top(); // Get the item with the highest value-to-weight ratio
            pq.pop(); // Remove the item from the priority queue
            int index = it.second; // Get the index of the item
            double ratio = it.first; // Get the value-to-weight ratio of the item
            
            // If the item's weight is less than or equal to the remaining weight capacity of the knapsack
            if(remWt >= arr[index].weight){
                totalValue += arr[index].value; // Add the item's value to the total value
                remWt -= arr[index].weight; // Subtract the item's weight from the remaining weight capacity
            }
            else {
                // If the item's weight is more than the remaining weight capacity of the knapsack
                totalValue += remWt * ratio; // Add the fraction of the item's value to the total value
                remWt = 0; // Set the remaining weight capacity to 0
            }
        }
        
        return totalValue; // Return the maximum total value that can be put in the knapsack  
    }
};
```
