### [Shortest Job first](https://www.geeksforgeeks.org/problems/shortest-job-first/1)

### Approach and Intuition

The given function `solve` is designed to solve a problem where we need to find a specific type of average based on the burst times of processes, commonly seen in scheduling problems. Here's a detailed breakdown of the approach and intuition behind the main logic of the code:

1. **Initialization**:
   - The function receives a vector `bt` containing the burst times of processes.
   - The size of the vector is stored in the variable `n`.

2. **Sorting**:
   - The burst times in the vector `bt` are sorted in non-decreasing order using the `sort` function.
   - Sorting helps in systematically calculating the cumulative burst times, which is essential for calculating the average waiting time in scheduling algorithms.

3. **Variable Setup**:
   - Several variables are initialized:
     - `average`: This will store the cumulative sum that contributes to the final average calculation.
     - `curr`: This holds the burst time of the current process being considered.
     - `prevSum`: This keeps track of the cumulative sum of burst times up to the previous process.

4. **Iterating through Burst Times**:
   - The function iterates through the burst times, excluding the last one (`for(int i=0; i < n-1; i++)`):
     - `curr` is set to the current burst time (`bt[i]`).
     - `average` is incremented by the sum of `curr` and `prevSum`.
     - `prevSum` is updated to include `curr`.

5. **Calculating the Average**:
   - After iterating through the burst times, `average` contains the cumulative sum of waiting times.
   - The `average` is divided by `n` to get the average waiting time for the processes.

6. **Returning the Result**:
   - The function returns the calculated average.

### Detailed Explanation

The function aims to compute the average waiting time for processes based on their burst times, which is a common problem in CPU scheduling algorithms. Here's a more in-depth explanation of each step:

1. **Sorting**:
   - Sorting the burst times is crucial as it allows us to systematically calculate the waiting times in a manner that minimizes the overall waiting time. This approach is aligned with the Shortest Job First (SJF) scheduling algorithm, which is optimal for minimizing average waiting time.

2. **Cumulative Sum Calculation**:
   - By iterating through the sorted burst times, the function keeps a running total of the previous burst times (`prevSum`). This helps in calculating the waiting time for each subsequent process.
   - For each process \(i\), the waiting time is essentially the sum of all previous burst times. This is accumulated in the `average` variable.

3. **Dividing by the Number of Processes**:
   - Once the total waiting time is calculated, dividing by the number of processes (`n`) gives the average waiting time. This average is essential in evaluating the efficiency of a scheduling algorithm.

### Summary
The function `solve` efficiently calculates the average waiting time for a set of processes given their burst times. By sorting the burst times and using a cumulative sum approach, it ensures that the waiting times are minimized in line with the principles of the Shortest Job First scheduling algorithm. The time complexity is dominated by the sorting step (\(O(n \log n)\)), and the space complexity is minimal (\(O(1)\) excluding the sort operation). This approach provides a clear and systematic way to determine the average waiting time, which is critical in optimizing CPU scheduling.
## Time and Space Complexity:
### Time Complexity:
- The time complexity of this function is \(O(n \log n)\) due to the sorting step. Sorting the burst times dominates the overall time complexity.
- The subsequent iteration through the burst times has a time complexity of \(O(n)\), but this is overshadowed by the sorting step.

### Space Complexity:
- The space complexity of the function is \(O(1)\) if we ignore the space required for sorting. Sorting typically requires \(O(\log n)\) extra space for the recursion stack (in case of the quicksort algorithm used by the C++ standard library), but this is still considered a minor overhead.

## Code:
```
#include <bits/stdc++.h>
using namespace std;
// } Driver Code Ends
// User function Template for C++
#include<vector>
// Back-end complete function Template for C++
class Solution {
  public:
    long long solve(vector<int>& bt) {
        // Get the size of the input vector
        int n = bt.size();
        
        // Sort the vector in ascending order
        sort(bt.begin(), bt.end());
        
        long long average = 0, curr = 0, prevSum = 0;
        
        // Iterate from the beginning to the second-last element
        for(int i=0; i<n-1; i++) {
            // Store the current element
            curr = bt[i];
            
            // Calculate the sum of all elements up to the current index
            // by adding the current element and the sum of previous elements
            average += curr + prevSum;
            
            // Update the sum of previous elements
            prevSum = curr + prevSum;
        }
        
        // Calculate the average by dividing the sum by the total number of elements
        average /= n;
        
        // Return the average
        return average;
    }
};
```
