### [Panagram Checking](https://www.geeksforgeeks.org/problems/pangram-checking-1587115620/1)

## Explanation:
1. **Class Definition**: The code defines a class named `Solution`. This is a common practice in C++, where you encapsulate related functions and data within a class.

2. **Function Declaration**: Inside the `Solution` class, there's a public function `checkPangram` that takes a string `s` as an argument and returns a boolean value. This function checks if the input string `s` is a pangram or not.

3. **Set Declaration**: A set `st` of type `char` is declared. In C++, a set is a container that stores unique elements following a specific order. Here, it's used to store each unique alphabetic character in the string.

4. **Loop Over String**: The function then loops over each character in the string `s`. For each character, it checks if it's an alphabetic character using the `isalpha` function. If it's not an alphabetic character, it continues to the next iteration.

5. **Character Insertion**: If the character is alphabetic, it's converted to lowercase using the `tolower` function and then inserted into the set `st`. The `tolower` function ensures that the check is case-insensitive.

6. **Pangram Check**: Finally, the function checks if the size of the set `st` is 26 (i.e., the number of letters in the English alphabet). If it is, the function returns `true`, indicating that the string is a pangram. Otherwise, it returns `false`.

## Time and Space Complexity:
### `Time Complexity`:
The time complexity of the function is O(n), where n is the size of the string. This is because the function needs to iterate over each character in the string once.

### `Space Complexity`:
The space complexity of the function is O(1). Although a set is used, the maximum size of the set is 26 (the number of letters in the English alphabet), which is a constant. Therefore, the space complexity is constant.

## Code:
```cpp
// User function template for C++

// Class definition for the solution
class Solution {
  public:
    // Function to check if a string is Pangram or not.
    bool checkPangram(string s) {
        
        // Set to store unique lowercase alphabets encountered in the string
        set<char> st;
        
        // Loop through each character in the string
        for (int i = 0; i < s.size(); i++) {
            
            // Check if the character is not an alphabet, and continue to the next iteration
            if (!isalpha(s[i])) continue;
            
            // Insert the lowercase version of the alphabet into the set
            st.insert(tolower(s[i]));
        }
        
        // Check if the size of the set is 26 (indicating all alphabets are present)
        return st.size() == 26;
    }
};

```
