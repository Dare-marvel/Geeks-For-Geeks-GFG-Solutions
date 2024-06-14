### [Minimum Platforms](https://www.geeksforgeeks.org/problems/minimum-platforms-1587115620/1)

### Approach and Intuition

1. **Understanding the Problem:**
   - You need to determine the minimum number of platforms required at a railway station so that no train has to wait.
   - Trains are represented by their arrival (`arr[]`) and departure (`dep[]`) times.
   - The goal is to find out the peak number of trains at the station at any given time.

2. **Sorting Arrival and Departure Times:**
   - The first step is to sort both the arrival and departure arrays.
   - Sorting helps us to efficiently count the number of overlapping trains at any given time.

3. **Using Two Pointers:**
   - Initialize two pointers: `arr_ptr` and `dep_ptr`, both set to 0.
   - These pointers will help in traversing the sorted arrival and departure arrays respectively.

4. **Counting Platforms Needed:**
   - Initialize `cnt` (to keep track of the current number of trains at the station) to 0.
   - Initialize `maxCnt` (to store the maximum number of platforms needed at any time) to a very small number (negative infinity).
   
5. **Traverse Through Both Arrays:**
   - Use a while loop to traverse the sorted arrays.
   - If the current arrival time (`arr[arr_ptr]`) is less than or equal to the current departure time (`dep[dep_ptr]`), it means a train has arrived before the previous train departs, so increment `cnt` and move the `arr_ptr` to the next train.
   - If the current arrival time is greater than the current departure time, it means a train has departed, so decrement `cnt` and move the `dep_ptr` to the next train.
   
6. **Updating the Maximum Count:**
   - After each comparison, update `maxCnt` to the maximum of `cnt` and `maxCnt`.
   - This ensures that `maxCnt` always holds the maximum number of trains at the station at any point in time.

7. **Returning the Result:**
   - Finally, return `maxCnt` as it represents the minimum number of platforms required so that no train has to wait.

## Time and Space Complexity

### **Time Complexity:**

- **Sorting the Arrays:** Sorting the arrival and departure arrays each takes \(O(n \log n)\).
- **Traversing the Arrays:** The while loop traverses both arrays once, resulting in \(O(n)\) time complexity.
- **Overall Time Complexity:** The overall time complexity is dominated by the sorting step, thus it is \(O(n \log n)\).

### **Space Complexity:**

- **Auxiliary Space:** The algorithm primarily uses a few extra variables for counting and tracking pointers. Therefore, the auxiliary space is \(O(1)\).
- **Sorted Arrays:** Although the sorted arrays consume space, this space is not extra as we are sorting the given input arrays in place.
- **Overall Space Complexity:** The overall space complexity is \(O(1)\).

### Summary

In essence, the algorithm efficiently determines the minimum number of platforms required by:
- Sorting the arrival and departure times,
- Using a two-pointer technique to traverse through these times,
- Counting the number of overlapping trains at the station, and
- Keeping track of the maximum number of trains present at any time to determine the peak requirement for platforms.

This approach ensures that the problem is solved in an optimal manner with \(O(n \log n)\) time complexity and \(O(1)\) space complexity.

## Code:
```cpp
class Solution{
    public:
    //Function to find the minimum number of platforms required at the
    //railway station such that no train waits.
    int findPlatform(int arr[], int dep[], int n)
    {
        // Sorting the arrival and departure arrays
    	sort(arr,arr+n);
    	sort(dep,dep+n);
    	
    	// Initializing pointers for arrival and departure arrays
    	int arr_ptr = 0, dep_ptr = 0;
    	
    	// Initializing counters for current platforms needed (cnt) and maximum platforms needed (maxCnt)
    	int cnt = 0, maxCnt = -1e9;
    	
    	// Looping through the arrival array
    	while(arr_ptr < n){
    	    // If the next train arrives before the current one departs, increment the counter and move to the next arrival
    	    if(arr[arr_ptr] <= dep[dep_ptr]){
    	        cnt++;
    	        arr_ptr++;
    	    }
    	    // If the next train arrives after the current one departs, decrement the counter and move to the next departure
    	    else {
    	        cnt--;
    	        dep_ptr++;
    	    }
    	    // Update the maximum platforms needed
    	    maxCnt = max(cnt,maxCnt);
    	}
    	
    	// Return the maximum platforms needed
    	return maxCnt;
    }
};
```
