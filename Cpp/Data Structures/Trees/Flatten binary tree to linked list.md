### [Flatten binary tree to linked list](https://www.geeksforgeeks.org/problems/flatten-binary-tree-to-linked-list/1?utm_source=geeksforgeeks&utm_medium=article_practice_tab&utm_campaign=article_practice_tab)

## [Explanation](https://takeuforward.org/data-structure/flatten-binary-tree-to-linked-list/)

## Code:
```cpp
class Solution
{
    // Using a global variable to keep track of the previous node in the flattened tree
    Node * prev = NULL;
    
public:
    // Function to flatten a binary tree into a right-skewed tree
    void flatten(Node *root)
    {
        // Base case: If the current node is NULL, return
        if(root == NULL) return;
        
        // Recursively flatten the right subtree
        flatten(root->right);
        
        // Recursively flatten the left subtree
        flatten(root->left);
        
        // Assign the previous node (rightmost node in the flattened tree) to the current node's right child
        root->right = prev;
        
        // Set the left child of the current node to NULL (as the tree is being flattened to the right)
        root->left = NULL;
        
        // Update the previous node to the current node for the next iteration
        prev = root;
    }
};
```
