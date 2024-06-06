### [Job Sequencing Problem](https://www.geeksforgeeks.org/problems/job-sequencing-problem-1587115620/1)

## Approach and Intuition of the Main Logic

The given code addresses the Job Scheduling problem with the goal of maximizing profit by scheduling jobs within their respective deadlines. Each job has a profit and a deadline, and we aim to perform as many jobs as possible within their deadlines to achieve the maximum profit. Here is a detailed breakdown of the approach and intuition behind the solution:

1. **Job Struct and Comparator:**
   - The `Job` struct has three attributes: `id` (job ID), `dead` (deadline), and `profit` (profit if completed before or on the deadline).
   - The `comparison` function is a custom comparator used to sort the jobs in descending order of their profit. This ensures that we consider the highest profit jobs first.

2. **Sorting Jobs by Profit:**
   - The jobs are sorted in descending order of profit using the `comparison` function. This is achieved through the `sort` function in C++.
   - Sorting ensures that we prioritize higher profit jobs when scheduling, leading to potentially higher total profit.

3. **Finding the Maximum Deadline:**
   - We iterate through the sorted jobs to find the maximum deadline (`max_dead`). This helps in determining the size of the slots array, which will be used to keep track of scheduled jobs.

4. **Slots Array Initialization:**
   - A `slots` array of size `max_dead + 1` is initialized with `-1`, indicating that initially, all slots are free. The array size is `max_dead + 1` because slots are indexed from 1 to `max_dead`.

5. **Job Scheduling:**
   - We iterate through the sorted jobs and try to schedule each job in the latest possible slot before its deadline.
   - For each job, we check slots from its deadline down to 1. If we find a free slot (`slots[j] == -1`), we assign the job to that slot.
   - We increment the `count` of scheduled jobs and add the job's profit to `TotalProfit`.

6. **Result Preparation:**
   - After scheduling all possible jobs, we store the `count` of scheduled jobs and the `TotalProfit` in a vector `ans`.
   - The function returns `ans`, which contains the number of jobs done and the total profit.

### Detailed Steps within the Code:

1. **Sort Jobs by Profit:**
   - `sort(arr, arr + n, comparison);` sorts the array `arr` based on the custom comparator, ensuring that jobs with higher profit come first.

2. **Find Maximum Deadline:**
   - `int max_dead = 0;` initializes the maximum deadline.
   - The loop `for(int i=0; i<n; i++) { max_dead = max(max_dead, arr[i].dead); }` updates `max_dead` to be the highest deadline among all jobs.

3. **Initialize Slots Array:**
   - `vector<int> slots(max_dead+1, -1);` creates an array `slots` of size `max_dead + 1` with all elements initialized to `-1`.

4. **Schedule Jobs:**
   - `for(int i=0; i<n; i++)` iterates through all jobs.
   - `for(int j=arr[i].dead; j>0; j--)` iterates backward from the job's deadline to 1.
   - If `slots[j] == -1`, the slot is free. Assign the job to this slot, increment the job count, and add the profit to `TotalProfit`.

5. **Return Result:**
   - `vector<int> ans; ans.push_back(count); ans.push_back(TotalProfit);` prepares the result vector.
   - `return ans;` returns the number of jobs done and the total profit.

## Time and Space Complexity

### **Time Complexity:**
  - Sorting the jobs takes \(O(n \log n)\).
  - Finding the maximum deadline takes \(O(n)\).
  - Scheduling jobs involves nested loops, where the outer loop runs \(n\) times and the inner loop runs at most `max_dead` times. In the worst case, this is \(O(n \times D)\), where `D` is the maximum deadline.
  - Overall, the time complexity is \(O(n \log n + n \times D)\). Since `D` can be up to `n`, it simplifies to \(O(n \log n + n^2)\), but in many practical scenarios, `D` is much smaller than `n`.

### **Space Complexity:**
  - The `slots` array has a size of `max_dead + 1`, resulting in \(O(D)\) space complexity.
  - Other variables use a constant amount of space.
  - Overall, the space complexity is \(O(D)\).

### Summary of the Approach:

1. **Sort jobs by profit in descending order**.
2. **Find the maximum deadline among all jobs**.
3. **Initialize a slots array to track job assignments**.
4. **Iterate through the jobs and assign each to the latest possible free slot before its deadline**.
5. **Count the number of jobs assigned and sum up the total profit**.
6. **Return the result with the number of jobs done and the total profit**.

This greedy approach efficiently schedules jobs to maximize profit within their deadlines, balancing complexity and practicality.

## Code:
```cpp
// Job structure to hold the job details
struct Job 
{ 
    int id;	 // Job Id 
    int dead; // Deadline of job 
    int profit; // Profit if job is over before or on deadline 
};

// Solution class to solve the job scheduling problem
class Solution 
{
    public:
    // Comparison function to sort jobs according to profit
    bool static comparison(Job a, Job b) {
         return (a.profit > b.profit);
    }
    
    // Function to find the maximum profit and the number of jobs done
    vector<int> JobScheduling(Job arr[], int n) 
    {
        // Sorting the jobs based on profit
        sort(arr, arr + n, comparison);
        
        // Finding the maximum deadline
        int max_dead = 0;
        for(int i=0; i<n; i++){
            max_dead = max(max_dead, arr[i].dead);
        }

        // Creating a slots vector to hold the jobs
        vector<int> slots(max_dead+1,-1);
        int TotalProfit=0,count=0;
        
        // Looping through the jobs
        for(int i=0;i<n;i++){
            // Finding a slot for the job
            for(int j=arr[i].dead;j>0;j--){
                // If the slot is empty
                if(slots[j] == -1){
                    // Assign the job to the slot
                    slots[j] = i;
                    // Increase the count of jobs
                    count++;
                    // Add the profit of the job to the total profit
                    TotalProfit += arr[i].profit;
                    break;
                }
            }
        }
        
        // Creating a vector to hold the answer
        vector<int> ans;
        // Adding the count of jobs to the answer
        ans.push_back(count);
        // Adding the total profit to the answer
        ans.push_back(TotalProfit);
        
        // Returning the answer
        return ans;
    }
};
```
