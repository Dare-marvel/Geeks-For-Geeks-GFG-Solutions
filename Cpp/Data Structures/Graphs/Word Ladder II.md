### [Word Ladder II](https://www.geeksforgeeks.org/problems/word-ladder-ii/1)

## Explanation:
1. **Problem Overview**: The code addresses the problem of finding all possible sequences of words that can transform a given starting word (`beginWord`) into a target word (`endWord`) by changing only one letter at a time, with each intermediate word being present in a provided list of words (`wordList`).

2. **Data Structures**: The code utilizes several data structures:
   - `unordered_set<string>` (`st`) to efficiently store and look up words from `wordList`.
   - `queue<vector<string>>` (`q`) to perform a breadth-first search (BFS) on the sequences of words.
   - `vector<string>` (`usedOnLevel`) to keep track of words used in the current level of BFS.
   - `vector<vector<string>>` (`ans`) to store the final sequences found.

3. **Initialization**: 
   - Initialize the `unordered_set` with the words from `wordList`.
   - Create an empty queue (`q`) and push the starting word sequence (`beginWord`) into it.
   - Initialize `usedOnLevel` with the starting word.

4. **Breadth-First Search (BFS)**:
   - Perform BFS until the queue is empty.
   - Dequeue the front word sequence from the queue.
   - If the size of the word sequence exceeds the current level, update the level and remove words used in the current level from the set.
   - Check if the last word in the sequence is equal to the `endWord`. If so, add the sequence to `ans`.
   - Generate all possible words by changing one letter at a time and check if they are present in the set.
   - If a word is found in the set, add it to the sequence, push the updated sequence into the queue, mark the word as used for this level, and then remove it from the sequence.

5. **Result**: Return the final answer containing all possible sequences from `beginWord` to `endWord`.

**Approach Summary**:
- The code employs BFS to explore all possible sequences of words from the starting word to the target word, ensuring that each intermediate word is present in the provided word list.
- It maintains a set of unused words to optimize the search process and avoid revisiting the same words.
- By systematically exploring word transformations through BFS and keeping track of used words at each level, it efficiently finds all valid sequences.

## Time and Space Complexity:
### `Time Complexity`:
- The time complexity is proportional to the number of words in the word list and the length of each word, as BFS explores all possible word transformations.
- Let \( n \) be the number of words in the word list, and \( l \) be the length of each word. The worst-case time complexity is \( O(n \cdot l^2) \), where \( l^2 \) represents the nested loop to generate all possible word transformations.

### `Space Complexity`:
- The space complexity primarily depends on the size of the queue and the set of unused words.
- In the worst case, where all words in the word list are used and stored in the queue and set, the space complexity is \( O(n) \) for both the queue and the set.

## Code:
```cpp
// This is a C++ class named Solution. It's used to find sequences of words
// that can be transformed from a given 'beginWord' to an 'endWord' using
// transformations from a provided 'wordList'.
class Solution {
public:
    // Function to find sequences from beginWord to endWord
    vector<vector<string>> findSequences(string beginWord, string endWord, vector<string>& wordList) {
        // Create an unordered_set 'st' to efficiently check if a word is in 'wordList'
        unordered_set<string> st(wordList.begin(), wordList.end());
        
        // Create a queue 'q' to perform BFS
        queue<vector<string>> q;
        
        // Push the starting word sequence into the queue
        q.push({beginWord});
        
        // 'usedOnLevel' keeps track of words used in the current level of BFS
        vector<string> usedOnLevel;
        
        // Initialize 'usedOnLevel' with the starting word
        usedOnLevel.push_back({beginWord});
        
        // 'level' keeps track of the current level of BFS
        int level = 0;
        
        // 'ans' will store the final sequences found
        vector<vector<string>> ans;
        
        // BFS loop
        while(!q.empty()){
            // Dequeue the front word sequence
            vector<string> vec = q.front();
            q.pop();
            
            // If the size of the word sequence is greater than the current level, update the level
            if(vec.size() > level){
                level++;
                // Remove words used in the current level from the set
                for(auto it:usedOnLevel){
                    st.erase(it);
                }
            }
            
            // Get the last word in the sequence
            string word = vec.back();
            
            // Check if the last word is the endWord
            if(word == endWord){
                // If ans is empty, add the sequence to ans
                if(ans.size() == 0){
                    ans.push_back(vec);
                }
                // If ans is not empty and the sequence size matches, add the sequence to ans
                else if(ans[0].size() == vec.size()){
                    ans.push_back(vec);
                }
            }
            
            // Generate all possible words by changing one character at a time
            for(int i=0;i<word.size();i++){
                char original = word[i];
                
                for(char ch='a';ch<='z';ch++){
                    word[i] = ch;
                    
                    // If the generated word is in the set, add it to the queue and mark it as used for this level
                    if(st.count(word) > 0){
                        vec.push_back(word);
                        q.push(vec);
                        usedOnLevel.push_back(word);
                        vec.pop_back();
                    }
                }
                
                // Revert the word back to its original state
                word[i] = original;
            }
            
        }
        
        // Return the final answer
        return ans;
    }
};
```
