### [Subset Sum Problem](https://practice.geeksforgeeks.org/problems/subset-sum-problem-1611555638/1?utm_source=geeksforgeeks&utm_medium=article_practice_tab&utm_campaign=article_practice_tab)

## Explanation:
Sure, let's break down the code and dry run it with a more detailed example. Let's say we have an array `arr = [2, 3, 7, 8, 10]` and we want to find if there's a subset that sums up to `11`.

1. **Initialization**: We start by initializing `n` to the size of `arr`, which is `5`. Also, initialize `sum` to `11`.

2. **DP Table Creation**: We create a 2D DP array `dp` with dimensions `(n+1) x (sum+1)`. All elements are initially `false`.

3. **DP Table Initialization**: We initialize the first column of `dp` to `true` because an empty subset always has sum `0`.

4. **Filling the DP Table**: Now, we start filling the `dp` table row by row (outer loop for `i` from `1` to `n`) and within each row, column by column (inner loop for `j` from `1` to `sum`).

5. **DP Table Update**: For each cell `dp[i][j]`, we check if `arr[i-1]` (the current element in the array) is less than or equal to `j` (the current sum). If it is, we set `dp[i][j]` to the logical OR of `dp[i-1][j-arr[i-1]]` (which represents the case where we include `arr[i-1]` in the subset) and `dp[i-1][j]` (which represents the case where we exclude `arr[i-1]` from the subset).

6. **Excluding Larger Elements**: If `arr[i-1]` is greater than `j`, we set `dp[i][j]` to `dp[i-1][j]`, which means we can't include `arr[i-1]` in the subset and the best we can do is the best we could do without `arr[i-1]`.

7. **Final Result**: After filling up the `dp` table, we return `dp[n][sum]`. This represents whether there's a subset of `arr` that sums up to `sum`.

Now, let's dry run this code with our example `arr = [2, 3, 7, 8, 10]` and `sum = 11`.

- After initialization, our `dp` table looks like this:

|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 |
|---|---|---|---|---|---|---|---|---|---|---|---|----|
| 0 | T | F | F | F | F | F | F | F | F | F | F  | F  |
| 1 |   |   |   |   |   |   |   |   |   |   |   |    |
| 2 |   |   |   |   |   |   |   |   |   |   |   |    |
| 3 |   |   |   |   |   |   |   |   |   |   |   |    |
| 4 |   |   |   |   |   |   |   |   |   |   |   |    |
| 5 |   |   |   |   |   |   |   |   |   |   |   |    |

- After filling the `dp` table, it looks like this:

|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 |
|---|---|---|---|---|---|---|---|---|---|---|---|----|
| 0 | T | F | F | F | F | F | F | F | F | F | F  | F  |
| 1 | T | F | T | F | F | F | F | F | F | F | F  | F  |
| 2 | T | F | T | T | F | T | F | F | F | F | F  | F  |
| 3 | T | F | T | T | F | T | F | T | F | T | F  | T  |
| 4 | T | F | T | T | F | T | F | T | T | T | T  | T  |
| 5 | T | F | T | T | F | T | F | T | T | T | T  | T  |

- The final result is `dp[5][11]` which is `true`, indicating that there's a subset of `arr` that sums up to `11`. In fact, the subset `{3, 8}` does sum up to `11`.

This dynamic programming approach ensures that each subproblem is solved only once, and the results are stored and reused in the `dp` table, which makes it more efficient than the recursive approach. This is more efficient than the original recursive approach, especially when the target sum is large.
## Time and Space Complexity:
### `Time Complexity`:  The time complexity of this code is **O(n*sum)**, where **n** is the size of the given set and **sum** is the target sum.

### `Space Complexity`: The space complexity is also **O(n*sum)**, as that's the space required for the `dp` table.

## Code:
```cpp
// Define a class named 'Solution'
class Solution{   
public:
    // Function to check if there is a subset of the array with a given sum
    bool isSubsetSum(vector<int> arr, int sum){
        // Get the size of the array
        int n = arr.size();

        // Create a 2D DP array with dimensions (n+1) x (sum+1) to store intermediate results
        vector<vector<bool>> dp(n+1, vector<bool>(sum+1, false));

        // Initialization: there is always a subset with sum 0
        for(int i=0; i<=n; i++)
            dp[i][0] = true;

        // Dynamic Programming loop to fill the DP array
        for(int i=1; i<=n; i++){
            for(int j=1; j<=sum; j++){
                // Check if the current element can be included in the subset with the remaining sum
                if(arr[i-1] <= j)
                    // Include the current element or exclude it to get the subset sum
                    dp[i][j] = dp[i-1][j-arr[i-1]] || dp[i-1][j];
                else
                    // If the current element is greater than the remaining sum, exclude it
                    dp[i][j] = dp[i-1][j];
            }
        }

        // The final result is stored in the bottom-right cell of the DP array
        return dp[n][sum];
    }
};

```
