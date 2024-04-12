### [Word Ladder I](https://www.geeksforgeeks.org/problems/word-ladder/1)

## Approach and Intuition:

1. **Breadth-First Search (BFS):**
   - The code utilizes the BFS algorithm to find the shortest transformation sequence from the `startWord` to the `targetWord`.
   - BFS is well-suited for such problems where the shortest path needs to be found in unweighted graphs or networks.
   
2. **Queue-Based Traversal:**
   - BFS involves traversing the graph level by level, expanding the search from the initial node outward.
   - A queue is used to manage the traversal, ensuring nodes are processed in the order they are discovered.

3. **Word Transformations:**
   - Starting from the `startWord`, each possible transformation is explored by changing one character at a time.
   - For each character position in the word, all lowercase alphabets are tried to generate new words.

4. **HashSet for Efficient Lookup:**
   - A HashSet (`unordered_set` in C++) is used to store the words from `wordList` for efficient lookup.
   - This helps in checking if a word is present in the `wordList` and avoids visiting the same word multiple times.

5. **Termination Condition:**
   - The process continues until the queue becomes empty or the `targetWord` is found.
   - If the `targetWord` is found, the corresponding step count (number of transformations) is returned.

## Time and Space Complexity:
### `Time Complexity`:
- **BFS Traversal:** 
  - In the worst-case scenario, every word in the `wordList` needs to be explored.
  - Each word has a length \(M\), and for each word, \(M\) transformations are attempted.
  - So, the time complexity of BFS traversal is \(O(N \times M)\), where \(N\) is the number of words in the `wordList`.
  
### `Space Complexity`:
- **Queue and HashSet:**
  - The space complexity primarily depends on the space required for the queue and the HashSet.
  - The queue may hold \(N\) elements at most, where \(N\) is the number of words in `wordList`.
  - The HashSet stores the words from `wordList`, which also requires \(O(N \times M)\) space in the worst case.
  - So, the overall space complexity is \(O(N \times M)\).
  
## Code:
```cpp
class Solution {
public:
    // Function to find the length of the shortest transformation sequence from startWord to targetWord
    int wordLadderLength(string startWord, string targetWord, vector<string>& wordList) {
        // Initialize a queue to perform BFS traversal
        queue<pair<string,int>> q; // Each element of the queue is a pair of string (word) and integer (steps)
        
        // Enqueue the startWord with initial step count 1
        q.push({startWord, 1});
        
        // Convert wordList to an unordered_set for efficient lookup and remove startWord
        unordered_set<string> st(wordList.begin(), wordList.end());
        st.erase(startWord);
        
        // Perform BFS traversal
        while (!q.empty()) {
            // Extract the current word and its step count from the front of the queue
            string word = q.front().first;
            int steps = q.front().second;
            
            // Remove the processed element from the queue
            q.pop();
            
            // If the current word is equal to the targetWord, return the steps
            if (word == targetWord) 
                return steps;
            
            // Generate all possible next words by changing one character at a time
            for (int i = 0; i < word.size(); i++) {
                char original = word[i]; // Store the original character
                
                // Try replacing the current character with all lowercase alphabets
                for (char ch = 'a'; ch <= 'z'; ch++) {
                    word[i] = ch; // Change the character at index i
                    
                    // If the generated word exists in the wordList, remove it from the set and enqueue it
                    if (st.find(word) != st.end()) {
                        st.erase(word); // Remove the word from the set to avoid revisiting
                        q.push({word, steps + 1}); // Enqueue the word with incremented step count
                    }
                }
                
                word[i] = original; // Restore the original character at index i
            }
        }
        
        // If targetWord is not reachable from startWord, return 0
        return 0;
    }
};
```
