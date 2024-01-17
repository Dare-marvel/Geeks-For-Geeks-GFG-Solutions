### [Rod Cutting](https://www.geeksforgeeks.org/problems/rod-cutting0840/1?utm_source=geeksforgeeks&utm_medium=article_practice_tab&utm_campaign=article_practice_tab)

## [Explanation](https://takeuforward.org/data-structure/rod-cutting-problem-dp-24/)

## Tabulation:
```cpp
class Solution {
public:
    // Function to find the maximum obtainable value by cutting up the rod
    int cutRod(int price[], int n) {
        // Initialize a 2D vector for dynamic programming, representing the maximum value for each length and price
        vector<vector<int>> dp(n + 1, vector<int>(n + 1, 0));

        // Base case: when the length of the rod is 0, the value is 0 for any price
        for (int p = 0; p <= n; p++) {
            dp[0][p] = 0;
        }

        // Iterate over each possible rod length
        for (int ind = 1; ind <= n; ind++) {
            // Iterate over each possible price (or length of the rod for simplicity)
            for (int pr = 0; pr <= n; pr++) {
                // Calculate the value of not taking the current rod piece
                int notTake = dp[ind - 1][pr];

                // Calculate the value of taking the current rod piece
                int take = INT_MIN;
                
                // Check if the length of the current rod piece is less than or equal to the remaining length
                int rodL = ind;
                if (rodL <= pr) {
                    // Update the value if taking the current rod piece is profitable
                    take = price[ind - 1] + dp[ind][pr - rodL];
                }

                // Store the maximum value between taking and not taking the current rod piece
                dp[ind][pr] = max(take, notTake);
            }
        }

        // The result is stored in the bottom-right corner of the 2D array
        return dp[n][n];
    }
};

```

## Memoization:
```cpp
class Solution{
  public:
    int cutRodUtil(int price[],int ind,int N,vector<vector<int>> &dp){
        if(ind == 0) return N * price[0];
        
        if(dp[ind][N] != -1) return dp[ind][N];
        
        int notTake = cutRodUtil(price,ind-1,N,dp);
        int take = INT_MIN;
        
        int rodL= ind+1;
        if(rodL <= N) take = price[ind]+cutRodUtil(price,ind,N-rodL,dp);
        
        return dp[ind][N] = max(take,notTake);
    }
    int cutRod(int price[], int n) {
        vector<vector<int>> dp(n,vector<int>(n+1,-1));
        return cutRodUtil(price,n-1,n,dp);
    }
};
```

## Recursion (115 / 1115 testcases passed):
```cpp
class Solution{
  public:
    int cutRodUtil(int price[],int ind,int N){
        if(ind == 0) return N * price[0];
        
        int notTake = cutRodUtil(price,ind-1,N);
        int take = INT_MIN;
        
        int rodL= ind+1;
        if(rodL <= N) take = price[ind]+cutRodUtil(price,ind,N-rodL);
        
        return max(take,notTake);
    }
    int cutRod(int price[], int n) {
        return cutRodUtil(price,n-1,n);
    }
};
```
