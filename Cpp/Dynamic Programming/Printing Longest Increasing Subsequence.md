### [Printing Longest Increasing Subsequence](https://www.geeksforgeeks.org/problems/printing-longest-increasing-subsequence/1)

## Explanation:
1. **Class and Function Declaration**: The code is written in C++ and defines a class `Solution` with a public function `longestIncreasingSubsequence`. This function takes two parameters: an integer `n` representing the size of the array, and a vector `arr` of integers representing the array itself.

2. **Dynamic Programming Array Initialization**: Two vectors, `dp` and `hash`, of size `n` are initialized. `dp` is filled with 1s, representing the length of the longest increasing subsequence ending at each index. `hash` is used to keep track of the previous index in the longest increasing subsequence.

3. **Main Logic**: The main logic of the function is implemented using two nested loops. The outer loop iterates over the array from left to right. For each element, the inner loop checks all previous elements.

    - If the current element is greater than a previous element and the length of the longest increasing subsequence ending at the previous element plus one is greater than the current longest increasing subsequence length, then update the `dp` and `hash` arrays.
    - The `hash` array stores the index of the previous element in the longest increasing subsequence.
    - If the length of the longest increasing subsequence ending at the current index is greater than the maximum length found so far, update the maximum length and the last index of the longest increasing subsequence.

4. **Building the Longest Increasing Subsequence**: After finding the last index of the longest increasing subsequence, the code constructs the subsequence in reverse order by following the indices stored in the `hash` array. The subsequence is then reversed to get the correct order.

5. **Return Statement**: Finally, the function returns the longest increasing subsequence.

## Time and Space Complexity:
### `Time Complexity`:
The time complexity of the code is **O(n^2)**, where `n` is the size of the input array. This is because there are two nested loops iterating over the array.

### `Space Complexity`:
The space complexity of the code is **O(n)**, where `n` is the size of the input array. This is due to the additional space required for the `dp` and `hash` arrays.

## Code:
```cpp
// This code defines a class Solution with a public method longestIncreasingSubsequence.
// It takes an integer n and a vector of integers arr as input.
// The goal is to find the longest increasing subsequence in the given array.
// The code uses dynamic programming to track the length of the increasing subsequence ending at each index.
// It also maintains an array 'hash' to store the previous index in the subsequence.
// The variable 'maxi' keeps track of the maximum length, and 'lastIndex' stores the last index of the longest subsequence.

class Solution {
public:
    vector<int> longestIncreasingSubsequence(int n, vector<int>& arr) {
        vector<int> dp(n, 1), hash(n);
        int maxi = 1;
        int lastIndex = 0;

        // Loop through each element in the array
        for (int i = 0; i < n; i++) {
            hash[i] = i;

            // Check previous elements to find the longest increasing subsequence
            for (int prev = 0; prev < i; prev++) {
                if (arr[prev] < arr[i] && 1 + dp[prev] > dp[i]) {
                    dp[i] = 1 + dp[prev];
                    hash[i] = prev;
                }
            }

            // Update the maximum length and last index
            if (dp[i] > maxi) {
                maxi = dp[i];
                lastIndex = i;
            }
        }

        // Reconstruct the longest increasing subsequence
        vector<int> temp;
        temp.push_back(arr[lastIndex]);

        // Trace back through the 'hash' array to find the entire subsequence
        while (hash[lastIndex] != lastIndex) {
            lastIndex = hash[lastIndex];
            temp.push_back(arr[lastIndex]);
        }

        // Reverse the vector to get the correct order
        reverse(temp.begin(), temp.end());
        return temp;
    }
};
```
