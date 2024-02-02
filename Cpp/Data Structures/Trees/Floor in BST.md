### [Floor in BST](https://www.geeksforgeeks.org/problems/floor-in-bst/1)

## [Explanation](https://takeuforward.org/binary-search-tree/floor-in-a-binary-search-tree/)

## Code:
```cpp
// Class named Solution
class Solution{
public:
    // Function to find the largest value in the binary search tree that is smaller than or equal to a given input value
    int floor(Node* root, int input) {
        // If the root is NULL, return -1 indicating that there is no floor value
        if (root == NULL) return -1;

        // Initialize the answer variable to -1 (default if the input is smaller than all elements in the tree)
        int ans = -1;

        // Loop until either the root becomes NULL or the input value is found
        while(root){
            // If the input value is equal to the current node's data, the floor value is the input itself
            if(input == root->data){
                ans = input;
                return ans;
            }
            // If the input value is greater than the current node's data, update the floor value and move to the right subtree
            else if(root->data < input){
                ans = root->data;
                root = root->right;
            }
            // If the input value is smaller than the current node's data, move to the left subtree
            else{
                root = root->left;
            }
        }
    
        // Return the final floor value found
        return ans;
    }
};

```
