### [Boundary Traversal of binary tree](https://www.geeksforgeeks.org/problems/boundary-traversal-of-binary-tree/1?utm_source=geeksforgeeks&utm_medium=article_practice_tab&utm_campaign=article_practice_tab)

## Explanation:
Sure, let's break down this C++ code which is designed to find the boundary of a binary tree:

1. **Class and Function Definitions**: The code defines a class `Solution` with several public member functions. These functions work together to find and return the boundary of a binary tree.

2. **isLeaf Function**: This function checks if a given node is a leaf node. A node is considered a leaf node if it does not have any children (i.e., both its left and right pointers are null).

3. **addLeftBoundary Function**: This function traverses the left boundary of the binary tree. It starts from the root's left child and keeps going left if possible; if not, it goes right. It adds each non-leaf node to the result vector.

4. **addRightBoundary Function**: This function traverses the right boundary of the binary tree in a similar manner to the left boundary. However, it stores the nodes in a temporary vector first because they are encountered in bottom-up order. After the traversal, it reverses the temporary vector and adds its elements to the result vector.

5. **addLeaves Function**: This function adds all the leaf nodes in the binary tree to the result vector. It uses a simple recursive approach to traverse all nodes and checks if a node is a leaf node using the `isLeaf` function.

6. **boundary Function**: This is the main function that utilizes all the above functions to find the boundary of the binary tree. It first checks if the root is null or a leaf node. If not, it adds the root to the result vector. Then it calls `addLeftBoundary`, `addLeaves`, and `addRightBoundary` in order to add the left boundary, leaves, and right boundary to the result vector, respectively.

## Time and Space Complexity:
### `Time Complexity`:
In terms of time complexity, the code visits each node in the binary tree exactly once. Therefore, the time complexity is **O(n)**, where **n** is the number of nodes in the binary tree.

### `Space Complexity`:
As for space complexity, the code uses a vector to store the boundary nodes. In the worst case, the boundary can include all nodes of the tree (consider a skewed tree). Therefore, the space complexity is also **O(n)**.

## Code:
```cpp
class Solution {
public:
    // Function to check if a given node is a leaf
    bool isLeaf(Node *node) {
        return node && !node->left && !node->right;
    }

    // Function to add the left boundary of the tree to the result vector
    void addLeftBoundary(Node *root, vector<int> &res) {
        Node *curr = root->left;
        while (curr) {
            if (!isLeaf(curr)) {
                res.push_back(curr->data); // Add non-leaf node to result
            }
            if (curr->left) {
                curr = curr->left;
            } else {
                curr = curr->right;
            }
        }
    }

    // Function to add the right boundary of the tree to the result vector
    void addRightBoundary(Node *root, vector<int> &res) {
        Node *curr = root->right;
        vector<int> temp;
        while (curr) {
            if (!isLeaf(curr)) {
                temp.push_back(curr->data); // Add non-leaf node to temporary vector
            }
            if (curr->right) {
                curr = curr->right;
            } else {
                curr = curr->left;
            }
        }

        // Add the elements from the temporary vector in reverse order to the result vector
        for (int i = temp.size() - 1; i >= 0; i--) {
            res.push_back(temp[i]);
        }
    }

    // Function to add the leaves of the tree to the result vector
    void addLeaves(Node *root, vector<int> &res) {
        if (isLeaf(root)) {
            res.push_back(root->data); // Add leaf node to result
            return;
        }
        if (root->left) {
            addLeaves(root->left, res);
        }
        if (root->right) {
            addLeaves(root->right, res);
        }
    }

    // Function to get the boundary elements of the binary tree
    vector<int> boundary(Node *root) {
        vector<int> res;
        if (!root) {
            return res; // Return empty vector if the tree is empty
        }
        if (!isLeaf(root)) {
            res.push_back(root->data); // Add root if it is not a leaf
        }
        addLeftBoundary(root, res);
        addLeaves(root, res);
        addRightBoundary(root, res);
        return res; // Return the result vector containing the boundary elements
    }
};
```
