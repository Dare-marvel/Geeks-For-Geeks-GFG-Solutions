### [Party of Couples](https://www.geeksforgeeks.org/problems/alone-in-couple5507/1)

## Approach and Intuition:
1. **Problem Statement**: The code is designed to find the single element in an array where every other element appears twice. This is a common problem in computer science and is often solved using bitwise operations.

2. **Approach**: The code uses the XOR (exclusive OR) operation to solve this problem. The XOR operation has two important properties: (a) the XOR of a number with itself is 0, and (b) the XOR of a number with 0 is the number itself.

3. **Function (`findSingle`)**: This function takes an array `arr` of `n` integers as input. It initializes a variable `single_person` to 0. It then iterates over all elements in the array. For each element, it performs the XOR operation with `single_person`. Due to the properties of XOR, all elements appearing twice will eventually XOR to 0, leaving `single_person` as the single element that appears only once.

4. **Intuition**: The intuition behind this approach is that pairs of identical numbers will cancel each other out in the XOR operation, leaving only the single number that doesn't have a pair. This is a clever use of bitwise operations to solve a problem that would otherwise require extra space to solve.

## Time and Space Complexity:
### `Time Complexity`:
The time complexity of the code is O(n), where n is the number of elements in the array. This is because the code iterates over the array once.

### `Space Complexity`:
The space complexity of the code is O(1). This is because the code uses a fixed amount of space to store the `single_person` variable. It does not use any additional space that scales with the size of the input array.

## Code:
```py
class Solution:
    def findSingle(self, n, arr):
        # Initialize result with 0, as 0 is neutral in XOR operation
        single_person = 0
        
        # XOR all elements of the array; pairs will cancel out each other
        for person in arr:
            single_person ^= person
        
        return single_person

```
