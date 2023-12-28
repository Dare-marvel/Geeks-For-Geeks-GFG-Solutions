### [Minimal Cost](https://practice.geeksforgeeks.org/problems/minimal-cost/1?utm_source=geeksforgeeks&utm_medium=ml_article_practice_tab&utm_campaign=article_practice_tab)

## Explanation:
This C++ code is a solution to the problem of finding the minimum total cost for a frog to reach the top of a set of heights, where the frog can either jump one or two steps at a time, and the cost of each jump is the absolute difference in heights. The solution uses dynamic programming to optimize the process. Here's a detailed explanation:

1. **Including Libraries**: The code begins with `#include <bits/stdc++.h>`, which is a header file in C++ that includes most standard library files.

2. **Helper Function**: A helper function named `helper` is defined, which takes an index `ind`, a reference to a vector of integers `heights`, and a reference to a vector of integers `dp`. This function is used to calculate the minimum cost for the frog to reach the height at index `ind`.

3. **Base Case**: If `ind` is 0, the function returns 0. This is because if the frog is already at the first height, no jumps are needed, so the cost is 0.

4. **Memoization**: If `dp[ind]` is not -1, the function returns `dp[ind]`. This is because the minimum cost for the frog to reach the height at index `ind` has already been calculated and stored in `dp[ind]`.

5. **Recursive Case**: If `dp[ind]` is -1, the function calculates two possible costs: `left` and `right`. `left` is the cost of jumping from the previous height, which is the cost of reaching the previous height plus the absolute difference in heights. `right` is the cost of jumping from the height before the previous height, which is the cost of reaching that height plus the absolute difference in heights. However, `right` is only calculated if `ind` is greater than 1, because the frog can't jump two steps from the first height.

6. **Minimum Cost and Memoization**: The function returns the minimum of `left` and `right`, which is the minimum cost for the frog to reach the height at index `ind`. This minimum cost is also stored in `dp[ind]` for future reference.

7. **frogJump Function**: The `frogJump` function is defined, which takes an integer `n` and a reference to a vector of integers `heights`, and returns an integer. This function initializes a vector of integers `dp` with size `n+1` and all elements as -1, and then calls the `helper` function with `n-1` as the index, and returns the result. This is because the frog wants to reach the top, which is the last height in `heights`, and since indexing is 0-based, the index of the last height is `n-1`.

## Time and Space Complexity:
### `Time Complexity`:
The time complexity of the code is **O(n)**, because each height is visited once, and the minimum cost for each height is calculated once and stored in `dp`.

### `Space Complexity`:
The space complexity is also **O(n)**, because a vector of size `n+1` is used to store the minimum costs.

## Code:
```cpp
//{ Driver Code Starts
#include <bits/stdc++.h>
using namespace std;
// } Driver Code Ends

// Class definition for the Solution
class Solution {
  public:
    // Function to minimize the cost of jumping across a sequence of heights
    int minimizeCost(vector<int>& height, int n, int k) {
        // Code here

        // Vector to store minimum steps needed to reach each position
        vector<int> dp(n);
        dp[0] = 0; // Base case: Starting position requires 0 steps

        // Loop through each position starting from 1
        for(int i = 1; i < n; i++) {
            int minSteps = INT_MAX; // Initialize the minimum steps for the current position to a large value

            // Nested loop to explore possible jumps from the current position
            for(int j = 1; j <= k; j++) {
                // Check if jumping j positions back is within bounds
                if(i - j >= 0) {
                    // Calculate the cost of jumping to the current position from the previous position
                    int jump = dp[i - j] + abs(height[i] - height[i - j]);

                    // Update the minimum steps if the current jump is more optimal
                    minSteps = min(minSteps, jump);
                }
            }

            // Store the minimum steps needed to reach the current position in the dp vector
            dp[i] = minSteps;
        }

        // Return the minimum steps needed to reach the last position
        return dp[n - 1];
    }
};

//{ Driver Code Starts.

// Main function for testing the Solution class
int main() {
    int t;
    cin >> t;

    while (t--) {
        int N, K;
        cin >> N >> K;

        vector<int> arr(N);
        
        // Input heights of the sequence
        for (int i = 0; i < N; i++) {
            cin >> arr[i];
        }

        // Create an object of the Solution class
        Solution obj;

        // Call the minimizeCost function and print the result
        cout << obj.minimizeCost(arr, N, K) << "\n";
    }

    return 0;
}
// } Driver Code Ends

```
