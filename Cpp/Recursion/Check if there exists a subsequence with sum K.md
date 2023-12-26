## Code:
```cpp
class Solution{
    private:
    bool helper(int ind,vector<int>& arr,int k,int n,int curSum){
        if(ind == n){
            if(curSum == k){
                return true;
            }
            else{
                return false;
            }
        }
        
        if(curSum > k){
            return false;
        }
        
        curSum += arr[ind];
        if(helper(ind+1,arr,k,n,curSum) == true ) return true;
        
        curSum -= arr[ind];
        if(helper(ind+1,arr,k,n,curSum) == true) return true;
        
        return false;
        
    }
    public:
    bool checkSubsequenceSum(int n, vector<int>& arr, int k) {
        // Code here
        vector<int> ds;
        return helper(0,arr,k,n,0);
    }
};
```
