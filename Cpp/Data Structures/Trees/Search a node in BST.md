### [Search a node in BST](https://www.geeksforgeeks.org/problems/search-a-node-in-bst/1)

## [Explanation](https://takeuforward.org/binary-tree/search-in-a-binary-search-tree/)

## Code:
```cpp
// Function to search for a node with a given value in a binary search tree
bool search(Node* root, int x) {
    // Loop until either the root becomes NULL or the desired value is found
    while(root != NULL && root->data != x){
        // If the value to be searched is less than the current node's data, move to the left subtree
        // Otherwise, move to the right subtree
        root = x < root->data ? root->left : root->right;
    }
    // Return the result of the search (NULL if not found, the node if found)
    return root;
}
```
