### [Longest Bitonic subsequence](https://www.geeksforgeeks.org/problems/longest-bitonic-subsequence0824/1)

## [Explanation](https://takeuforward.org/data-structure/longest-bitonic-subsequence-dp-46/)

## Code:
```cpp
class Solution {
public:
    // Function to find the length of the Longest Bitonic Sequence in the given vector 'nums'
    int LongestBitonicSequence(vector<int> nums) {
        int n = nums.size();

        // Initialize an array 'dp1' to store the length of increasing subsequence ending at each index
        vector<int> dp1(n, 1);

        // Loop through the array to calculate increasing subsequence lengths
        for (int i = 0; i < n; i++) {
            for (int prev = 0; prev < i; prev++) {
                // Update the length if the current element is greater than the previous element
                // and the length including the previous element is greater than the current length
                if (nums[prev] < nums[i] && 1 + dp1[prev] > dp1[i])
                    dp1[i] = 1 + dp1[prev];
            }
        }

        // Initialize another array 'dp2' to store the length of decreasing subsequence starting at each index
        vector<int> dp2(n, 1);

        // Loop through the array in reverse to calculate decreasing subsequence lengths
        for (int i = n - 1; i >= 0; i--) {
            for (int prev = n - 1; prev > i; prev--) {
                // Update the length if the current element is greater than the previous element
                // and the length including the previous element is greater than the current length
                if (nums[prev] < nums[i] && 1 + dp2[prev] > dp2[i])
                    dp2[i] = 1 + dp2[prev];
            }
        }

        int maxi = 0;

        // Loop through the array to find the maximum length of bitonic sequence
        for (int i = 0; i < n; i++) {
            maxi = max(maxi, dp1[i] + dp2[i] - 1);
        }

        // Return the length of the Longest Bitonic Sequence
        return maxi;
    }
};

```
