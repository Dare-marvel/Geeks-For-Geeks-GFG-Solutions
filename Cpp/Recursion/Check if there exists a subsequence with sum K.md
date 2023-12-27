### [Check if there exists a subsequence with sum K](https://www.geeksforgeeks.org/problems/check-if-there-exists-a-subsequence-with-sum-k/1)

## Explanation:
This C++ code is a solution to the problem of checking if there exists a subsequence in an array whose sum equals a given number. Here's the detailed explanation:

1. **Class and Function Definitions**: The code defines a class `Solution` with a private helper function `helper` and a public function `checkSubsequenceSum`.

2. **Helper Function**: The `helper` function is a recursive function that checks if there exists a subsequence in the array `arr` starting from index `ind` whose sum equals `k`. It uses a variable `curSum` to keep track of the current sum of the subsequence.

3. **Base Cases**: The base cases for the recursion are when the index `ind` equals the size of the array `n` or when `curSum` exceeds `k`. If `ind` equals `n`, it checks if `curSum` equals `k` and returns the result. If `curSum` exceeds `k`, it returns false immediately as further recursion would only increase `curSum`.

4. **Recursive Calls**: The function makes two recursive calls for each element in the array - one includes the element in the subsequence (adds `arr[ind]` to `curSum`) and the other excludes it (leaves `curSum` unchanged). If either call returns true, the function returns true.

5. **Public Function**: The `checkSubsequenceSum` function is the main function that is called with the size of the array `n`, the array `arr`, and the target sum `k`. It calls the `helper` function with initial parameters and returns its result.

Please note that the keywords in the response are: `Solution`, `helper`, `checkSubsequenceSum`, `recursive`, `subsequence`, `array`, `curSum`, `base cases`, `recursive calls`, `time complexity`, and `space complexity`.

## Time and Space Complexity:
### `Time Complexity`:  The time complexity of the code is $$O(2^n)$$, where $$n$$ is the size of the array. This is because in the worst case, the code generates all possible subsequences of the array, which is exponential in the size of the array.

### `Space Complexity`: The space complexity of the code is $$O(n)$$, where $$n$$ is the size of the array. This is due to the recursive call stack that can go as deep as the size of the array in the worst case.

## Code:
```cpp
class Solution{
    private:
    // Helper function to recursively check for the subsequence sum
    bool helper(int ind, vector<int>& arr, int k, int n, int curSum){
        // Base case: If we have reached the end of the array
        if(ind == n){
            // Check if the current sum equals the target sum
            if(curSum == k){
                return true;
            } else {
                return false;
            }
        }

        // If the current sum exceeds the target sum, return false
        if(curSum > k){
            return false;
        }

        // Include the current element in the sum and check
        curSum += arr[ind];
        if(helper(ind+1, arr, k, n, curSum) == true) return true;

        // Exclude the current element from the sum and check
        curSum -= arr[ind];
        if(helper(ind+1, arr, k, n, curSum) == true) return true;

        // If including or excluding the current element does not result in the target sum, return false
        return false;
    }

    public:
    // Public function to check if there exists a subsequence with the given sum
    bool checkSubsequenceSum(int n, vector<int>& arr, int k) {
        // Initialize the helper function with initial parameters
        // Note: The initial current sum is set to 0
        return helper(0, arr, k, n, 0);
    }
};
```
