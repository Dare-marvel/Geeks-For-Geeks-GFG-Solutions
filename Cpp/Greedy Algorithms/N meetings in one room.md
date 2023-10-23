### [N meetings in one room](https://practice.geeksforgeeks.org/problems/n-meetings-in-one-room-1587115620/1)

## Explanation:
The code you've shared is a solution to the problem of scheduling the maximum number of meetings that can be held in a single room. Here's a detailed explanation of the logic:

1. **Meeting Structure**: The `meeting` structure is defined with three properties: `start`, `end`, and `pos`. These represent the start time, end time, and position of each meeting respectively.

2. **Comparator Function**: The `comparator` function is used to sort the meetings. It's a static function which means it can be called without an object. It sorts the meetings primarily by their end times in ascending order. If two meetings have the same end time, it sorts them by their position, prioritizing the one that comes first.

3. **maxMeetings Function**: This function is where the main logic of the program resides.
    - It first creates an array of `meeting` structures and initializes them with the start times, end times, and positions of the meetings.
    - It then sorts the `meeting` array using the `comparator` function.
    - It initializes a counter (`count`) to 1, representing the first meeting.
    - It sets a `limit` variable to the end time of the first meeting.
    - It then iterates over the rest of the meetings. If a meeting starts after the current `limit`, it updates the `limit` to that meeting's end time and increments the `count`.
    - Finally, it returns the `count`, which represents the maximum number of meetings that can be held.

4. **Main Function**: This function takes input for multiple test cases. For each test case, it takes input for the number of meetings (`n`), and their start and end times. It then creates an instance of the `Solution` class and calls its `maxMeetings` function with these inputs. The result is printed out.

## Time and Space Complexity:
### `Time Complexity`:
The time complexity is **O(n log n)** due to sorting operation where 'n' is number of meetings.

### `Space Complexity`:
The space complexity is **O(n)** as we are creating an array of structures for 'n' meetings.

## Code:
```cpp
// The given code represents a solution to the problem of finding the maximum number of meetings that can be performed in a meeting room.
// It uses a greedy approach to solve the problem efficiently.
// The code defines a structure 'meeting' to store information about each meeting, including its start and end times, and position.
// It sorts the meetings based on their end times in ascending order and, in case of a tie, based on their positions.
// The 'maxMeetings' function takes arrays of start and end times along with the number of meetings as input and returns the maximum number of meetings that can be conducted.

#include <bits/stdc++.h>
using namespace std;

// Definition of the meeting structure
struct meeting{
    int start;
    int end;
    int pos;
};

class Solution {
public:
    // Comparator function to sort meetings based on end times and positions
    static bool comparator(struct meeting m1, meeting m2){
        if (m1.end < m2.end) return true;
        else if (m2.end < m1.end) return false;
        else if (m1.pos < m2.pos) return true;
        return false;
    }
    
    // Function to find the maximum number of meetings that can be performed
    int maxMeetings(int start[], int end[], int n) {
        // Create an array of meetings using the given start and end times
        struct meeting meet[n];
        for(int i=0; i<n; i++){
            meet[i].start = start[i];
            meet[i].end = end[i];
            meet[i].pos = i+1;
        }
        
        // Sort meetings based on end times and positions using the comparator function
        sort(meet, meet+n, comparator);
        
        int count = 1; // Initialize count to keep track of meetings
        int limit = meet[0].end; // Initialize the end time of the first meeting
        
        // Iterate through sorted meetings and find maximum meetings that can be conducted
        for(int i=1; i<n; i++){
            // If the current meeting starts after the previous meeting ends, schedule it
            if(meet[i].start > limit){
                limit = meet[i].end; // Update the end time of the current meeting
                count++; // Increment the count of scheduled meetings
            }
        }
        
        return count; // Return the maximum number of meetings that can be conducted
    }
};

// Driver code to test the solution
int main() {
    int t;
    cin >> t;
    while (t--) {
        int n;
        cin >> n;
        int start[n], end[n];
        // Input start and end times of the meetings
        for (int i = 0; i < n; i++) cin >> start[i];
        for (int i = 0; i < n; i++) cin >> end[i];
        
        Solution ob; // Create a Solution object
        int ans = ob.maxMeetings(start, end, n); // Call the maxMeetings function to get the result
        cout << ans << endl; // Output the result (maximum meetings that can be conducted)
    }
    return 0;
}
```
