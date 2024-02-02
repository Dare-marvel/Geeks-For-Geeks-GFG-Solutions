### [Ceil in BST](https://www.geeksforgeeks.org/problems/implementing-ceil-in-bst/1)

## [Explanation](https://takeuforward.org/binary-search-tree/ceil-in-a-binary-search-tree/)

## Code:
```cpp
// Function to find the smallest value in the binary search tree that is greater than or equal to a given input value
int findCeil(Node* root, int input) {
    // If the root is NULL, return -1 indicating that there is no ceil value
    if (root == NULL) return -1;

    // Initialize the answer variable to -1 (default if the input is greater than all elements in the tree)
    int ans = -1;

    // Loop until either the root becomes NULL or the input value is found
    while(root){
        // If the input value is equal to the current node's data, the ceil value is the input itself
        if(input == root->data){
            ans = input;
            return ans;
        }
        // If the input value is greater than the current node's data, move to the right subtree
        else if(root->data < input){
            root = root->right;
        }
        // If the input value is smaller than the current node's data, update the ceil value and move to the left subtree
        else{
            ans = root->data;
            root = root->left;
        }
    }
    
    // Return the final ceil value found
    return ans;
}
```
