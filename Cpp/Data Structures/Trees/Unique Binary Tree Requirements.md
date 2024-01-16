### [Unique Binary Tree Requirements](https://geeksforgeeks.org/problems/unique-binary-tree-requirements/1)

## Explanation:

## Time and Space Complexity:
### `Time Complexity`:

### `Space Complexity`:

## Code:
```cpp
class Solution
{
public:
    bool isPossible(int a, int b)
    {
        return (a == 2) ^ (b == 2);
    }
};
```
