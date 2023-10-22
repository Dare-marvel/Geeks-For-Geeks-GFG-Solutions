### [Subset Sums](https://practice.geeksforgeeks.org/problems/subset-sums2234/1)

## Explanation:
1. **Class Definition**: The class `Solution` contains the solution to the problem.

2. **Function `func`**: This function is a recursive function that generates all possible subsets by making two choices at each step: either pick the current element and add it to the sum, or don't pick it. It then recursively calls itself for the next index and the updated sum.

3. **Function `subsetSums`**: This function initializes an empty vector `sumSubset` to store all possible subset sums, calls `func` to fill it, sorts it, and then returns it.

4. **Driver Code**: The driver code reads the input, calls `subsetSums` to get all possible subset sums, sorts them, and then prints them.

### `Time Complexity`:
The time complexity of this code is **O(2^N)** because in the worst case, there are 2^N possible subsets of an array of size N, and we generate all of them.

### `Space Complexity`:
The space complexity of this code is also **O(2^N)** because we store all possible subset sums in a vector. In the worst case, there are 2^N possible subsets and hence 2^N possible subset sums.
## Time and Space Complexity:

## Code:
```cpp
class Solution
{
public:
    // Recursive function to generate all subset sums
    void func(int ind, int sum, vector<int> &arr, int N, vector<int> &sumSubset)
    {
        // Base case: if index reaches N, add the current sum to the sumSubset vector
        if (ind == N)
        {
            sumSubset.push_back(sum);
            return;
        }
        
        // Recursive call: include the current element in the subset and move to the next index
        func(ind + 1, sum + arr[ind], arr, N, sumSubset);
        
        // Recursive call: exclude the current element from the subset and move to the next index
        func(ind + 1, sum, arr, N, sumSubset);
    }
    
    // Function to generate subset sums and return them in sorted order
    vector<int> subsetSums(vector<int> arr, int N)
    {
        // Vector to store generated subset sums
        vector<int> sumSubset;
        
        // Call the recursive function to generate subset sums starting from index 0 and sum 0
        func(0, 0, arr, N, sumSubset);
        
        // Sort the generated subset sums in ascending order
        sort(sumSubset.begin(), sumSubset.end());
        
        // Return the sorted subset sums
        return sumSubset;
    }
};
```
