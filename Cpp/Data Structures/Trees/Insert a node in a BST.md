### [Insert a node in a BST](https://www.geeksforgeeks.org/problems/insert-a-node-in-a-bst/1?utm_source=geeksforgeeks&utm_medium=ml_article_practice_tab&utm_campaign=article_practice_tab)

## [Explanation](https://www.log2base2.com/data-structures/tree/insert-a-node-in-binary-search-tree.html)

## Code:
```cpp
/*
   This code defines a binary tree node structure called 'Node', which contains an integer 'data',
   and pointers to the left and right child nodes.

   struct Node {
       int data;
       Node* left;
       Node* right;

       Node(int val) {
           data = val;
           left = right = NULL;
       }
   };
*/

class Solution
{
public:
    /*
       Function to insert a new node with data into a binary search tree.

       Parameters:
       - root: Pointer to the root node of the binary search tree.
       - data: Integer value to be inserted into the binary search tree.

       Returns:
       - Node pointer to the modified root of the tree.

       The function follows the binary search tree property, traversing the tree to find the
       appropriate position to insert the new node based on the comparison of data values.
       If the data is equal to the current node's data, it breaks out of the loop, handling the
       duplication case.

       Note: The code assumes that the provided Node structure is defined before this class.
    */
    Node* insert(Node* root, int data) {

        // If the tree is empty, create a new node with the given data as the root.
        if (root == NULL) return new Node(data);
        
        Node* curr = root;

        while (true) {
            // If data is greater, move to the right subtree.
            if (curr->data < data) {
                if (curr->right != NULL) curr = curr->right;
                else {
                    curr->right = new Node(data);
                    break;
                }
            }
            // If data is smaller, move to the left subtree.
            else if (curr->data > data) {
                if (curr->left != NULL) curr = curr->left;
                else {
                    curr->left = new Node(data);
                    break;
                }
            }
            // If data is equal, break out to handle duplication or modify as needed.
            else {
                // Handle the case where data is equal to the current node's data.
                // For simplicity, breaking out here.
                break;
            }
        }

        return root;
    }
};

```
