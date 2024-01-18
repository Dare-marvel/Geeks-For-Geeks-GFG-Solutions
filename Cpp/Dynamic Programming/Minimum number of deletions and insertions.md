### [Minimum number of deletions and insertions](https://www.geeksforgeeks.org/problems/minimum-number-of-deletions-and-insertions0209/1?utm_source=geeksforgeeks&utm_medium=article_practice_tab&utm_campaign=article_practice_tab)

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Code:
```cpp
class Solution{
public:
    // Function to calculate the length of the Longest Common Subsequence (LCS)
    int lcs(string s1, string s2) {
        int n = s1.size();
        int m = s2.size();
    
        // Create a 2D DP table with dimensions (n+1) x (m+1)
        vector<vector<int>> dp(n + 1, vector<int>(m + 1, -1)); // Initialize with -1
    
        // Initialize the base cases: LCS with an empty string is 0
        for (int i = 0; i <= n; i++) {
            dp[i][0] = 0;
        }
        for (int i = 0; i <= m; i++) {
            dp[0][i] = 0;
        }
    
        // Fill in the DP table to calculate the length of LCS
        for (int ind1 = 1; ind1 <= n; ind1++) {
            for (int ind2 = 1; ind2 <= m; ind2++) {
                if (s1[ind1 - 1] == s2[ind2 - 1])
                    dp[ind1][ind2] = 1 + dp[ind1 - 1][ind2 - 1]; // Characters match, increment LCS length
                else
                    dp[ind1][ind2] = max(dp[ind1 - 1][ind2], dp[ind1][ind2 - 1]); // Characters don't match, consider the maximum from left or above
            }
        }
    
        return dp[n][m]; // Return the length of the Longest Common Subsequence
    }

    // Function to calculate the minimum operations to make two strings equal
    int minOperations(string str1, string str2) { 
        // The minimum operations are equal to the sum of the lengths of both strings
        // minus twice the length of the LCS between the two strings
        return str1.size() + str2.size() - 2 * lcs(str1, str2);
    } 
};
```
