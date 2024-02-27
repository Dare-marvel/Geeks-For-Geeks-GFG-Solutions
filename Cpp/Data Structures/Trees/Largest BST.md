### [Largest BST](https://www.geeksforgeeks.org/problems/largest-bst/1?utm_source=geeksforgeeks&utm_medium=ml_article_practice_tab&utm_campaign=article_practice_tab)

## [Explanation](https://www.geeksforgeeks.org/largest-bst-binary-tree-set-2/)

## Code:
```cpp
/* Tree node structure used in the program */
struct Node {
    int data;
    Node *left;
    Node *right;

    Node(int val) {
        data = val;
        left = right = NULL;
    }
};

/* 
   NodeValue class is used to represent information about a subtree.
   It stores the minimum value, maximum value, and size of the BST within a subtree.
*/
class NodeValue {
public:
    int maxNode;   // Maximum value in the subtree
    int minNode;   // Minimum value in the subtree
    int maxSize;   // Size of the BST within the subtree

    // Constructor to initialize the NodeValue object
    NodeValue(int minNode, int maxNode, int maxSize) {
        this->minNode = minNode;
        this->maxNode = maxNode;
        this->maxSize = maxSize;
    }
};

/* Solution class contains the logic for finding the size of the largest BST within a binary tree */
class Solution {
public:
    // Recursive helper function to find the information about a subtree and return NodeValue
    NodeValue largestBSTSubtreeHelper(Node* root) {
        // Base case: If the root is null, return a NodeValue with invalid values
        if (!root) {
            return NodeValue(INT_MAX, INT_MIN, 0);
        }
        
        // Recursively find information about the left and right subtrees
        auto left = largestBSTSubtreeHelper(root->left);
        auto right = largestBSTSubtreeHelper(root->right);
        
        // Check if the current subtree rooted at 'root' is a valid BST
        if (left.maxNode < root->data && right.minNode > root->data) {
            // If valid, return NodeValue with updated values
            return NodeValue(min(root->data, left.minNode), max(root->data, right.maxNode), 1 + left.maxSize + right.maxSize);
        }
        
        // If the current subtree is not a valid BST, return NodeValue with invalid values
        return NodeValue(INT_MIN, INT_MAX, max(right.maxSize, left.maxSize));
    }

    /* You are required to complete this method */
    // Return the size of the largest sub-tree which is also a BST
    int largestBst(Node *root) {
        // Call the helper function to get information about the entire tree
        return largestBSTSubtreeHelper(root).maxSize;
    }
};

```
