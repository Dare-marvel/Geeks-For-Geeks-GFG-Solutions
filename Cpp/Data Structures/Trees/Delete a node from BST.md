### [Delete a node from BST](https://www.geeksforgeeks.org/problems/delete-a-node-from-bst/1?utm_source=geeksforgeeks&utm_medium=article_practice_tab&utm_campaign=article_practice_tab)

## Explanation:
1. **Struct Node**: This is a basic structure for a node in a binary search tree (BST). Each node contains an integer value (`data`), and two pointers (`left` and `right`) pointing to its left child and right child respectively. If a node does not have a left or right child, the corresponding pointer is `NULL`.

2. **Class Solution**: This class contains the method `deleteNode` which is used to delete a node from the BST.

3. **Method deleteNode**: This method takes two arguments - a pointer to the root node of the BST (`root`), and the data of the node to be deleted (`X`). The method returns a pointer to the root node of the BST after the deletion.

4. **Deletion Logic**: The method first checks if the BST is empty (i.e., `root == NULL`). If it is, it returns `NULL`. If the BST is not empty, it starts from the root node and traverses the BST to find the node to be deleted.

5. **Traversal**: The method uses a `while` loop for traversal. Inside the loop, it compares the data of the node to be deleted with the data of the current node (`root`). If the data to be deleted is less than the current data, it goes to the left subtree; if greater, it goes to the right subtree. If the data to be deleted is equal to the current data, it calls the `helper` function to delete the node and fix the BST.

6. **Method helper**: This method is used to delete a node (`root`) and fix the BST. It takes the node to be deleted as an argument and returns the new root of the subtree after the deletion. If the node to be deleted has no left child, it returns the right child; if it has no right child, it returns the left child. If the node to be deleted has both left and right children, it finds the rightmost node in the left subtree (`lastRight`), attaches the right child of the node to be deleted to the right of `lastRight`, and returns the left child of the node to be deleted.

7. **Method findLastRight**: This method is used to find the rightmost node in a subtree. It takes the root of the subtree as an argument and returns the rightmost node. It uses recursion to reach the rightmost node.

## Time and Space Complexity:
### `Time Complexity`:
The time complexity of the `deleteNode` method is O(h), where h is the height of the BST. This is because in the worst case, the method needs to traverse from the root to the deepest leaf node.

### `Space Complexity`:
The space complexity of the `deleteNode` method is O(h), because in the worst case, the depth of the recursive call stack can go up to h.
Please note that the time complexity can become O(n) in the worst case scenario where the BST degenerates into a linked list (i.e., every node has only one child). This can happen if the input data is sorted, causing all new nodes to be inserted as the right child of the deepest node. To avoid this worst case scenario, a self-balancing BST could be used.

## Code:
```cpp
// Forward declaration of helper functions
Node * helper(Node* root);
Node * findLastRight(Node* root);

// Function to delete a node from BST.
Node * deleteNode(Node * root, int X) {
    // If the tree is empty, return NULL (base case)
    if(root == NULL) return NULL;
    
    // If the current node contains the value to be deleted, call helper function to delete it
    if(root->data == X) return helper(root);
    
    // Save the root node in a dummy variable for later return
    Node * dummy = root;
    
    // Traverse the tree to find the node to be deleted
    while(root != NULL){
        // If the value to be deleted is less than the current node's value
        if(root->data > X){
            // If the left child exists and its value matches the value to be deleted
            if(root->left != NULL && root->left->data == X){
                // Call helper function to delete the node and update the left child
                root->left = helper(root->left);
                break;
            }
            else{
                // Move to the left child
                root = root->left;
            }
        }
        else{
            // If the right child exists and its value matches the value to be deleted
            if(root->right != NULL && root->right->data == X){
                // Call helper function to delete the node and update the right child
                root->right = helper(root->right);
                break;
            }
            else {
                // Move to the right child
                root = root -> right;
            }
        }
    }
    
    // Return the root of the tree after deletion
    return dummy;
}

// Helper function to delete a node from the BST
Node * helper(Node * root){
    // If the left child of the current node is NULL, return its right child
    if(root -> left == NULL){
        return root->right;
    }
    // If the right child of the current node is NULL, return its left child
    else if(root -> right == NULL){
        return root->left;
    }
    
    // Save the right child of the current node
    Node * rightChild = root->right;
    // Find the rightmost node in the left subtree of the current node
    Node * lastRight = findLastRight(root->left);
    
    // Connect the right child of the last right node in the left subtree to the right child of the current node
    lastRight -> right = rightChild;
    
    // Return the left child of the current node, which becomes the new subtree root after deletion
    return root->left;
}

// Function to find the rightmost node in a given subtree
Node * findLastRight(Node * root){
    // If the current node has no right child, it is the last right node
    if(root->right == NULL) return root;
    
    // Recursively find the rightmost node in the right subtree
    return findLastRight(root->right);
}

```
