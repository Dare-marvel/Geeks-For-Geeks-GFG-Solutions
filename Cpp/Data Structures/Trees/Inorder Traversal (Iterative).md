### [Inorder Traversal (Iterative)](https://www.geeksforgeeks.org/problems/inorder-traversal-iterative/1)

## [Explanation](https://takeuforward.org/data-structure/morris-inorder-traversal-of-a-binary-tree/)

## Code:
```cpp
/* Tree Node
struct Node {
    int data;
    Node* left;
    Node* right;
};*/

// Class definition for the solution
class Solution {
public:
    // Function to perform in-order traversal without using recursion
    vector<int> inOrder(Node* root) {
        // Vector to store the in-order traversal result
        vector<int> inorder;
        
        // Pointer to the current node, initially set to the root
        Node* curr = root;

        // Loop until the current node is not NULL
        while (curr != NULL) {
            // If the left child is NULL, visit the current node and move to the right child
            if (curr->left == NULL) {
                inorder.push_back(curr->data);
                curr = curr->right;
            } else {
                // If the left child is not NULL, find the rightmost node in the left subtree
                Node* prev = curr->left;
                while (prev->right && prev->right != curr) {
                    prev = prev->right;
                }

                // If the rightmost node's right child is NULL, set it to the current node
                // and move to the left child
                if (prev->right == NULL) {
                    prev->right = curr;
                    curr = curr->left;
                } else {
                    // If the rightmost node's right child is already set to the current node,
                    // reset it to NULL, visit the current node, and move to the right child
                    prev->right = NULL;
                    inorder.push_back(curr->data);
                    curr = curr->right;
                }
            }
        }

        // Return the in-order traversal result
        return inorder;
    }
};

```
