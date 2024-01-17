### [Rod Cutting](https://www.geeksforgeeks.org/problems/rod-cutting0840/1?utm_source=geeksforgeeks&utm_medium=article_practice_tab&utm_campaign=article_practice_tab)

## [Explanation](https://takeuforward.org/data-structure/rod-cutting-problem-dp-24/)

## Tabulation:
```

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
