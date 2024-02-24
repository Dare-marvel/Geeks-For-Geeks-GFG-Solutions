### [Inorder Successor in BST](https://www.geeksforgeeks.org/problems/inorder-successor-in-bst/1)

## Explanation:
Sure, here's a detailed explanation of the code:

1. **Struct Node**: This is a definition of a binary tree node. Each node has an integer value (`data`), a left child (`left`), and a right child (`right`). The constructor `Node(int val)` initializes a new node with the given value and sets the left and right children to `NULL`.

2. **Class Solution**: This class contains the main logic of the program. It has one public method: `inOrderSuccessor`.

3. **inOrderSuccessor Method**: This method finds the in-order successor of a given node `x` in a binary search tree rooted at `root`. The in-order successor of a node in a binary search tree is the node with the smallest value that is larger than the value of the given node.

4. **Successor Initialization**: A `Node` pointer `successor` is initialized to `NULL`. This will eventually point to the in-order successor of the node `x`.

5. **While Loop**: The method enters a while loop that continues as long as `root` is not `NULL`. This loop traverses the binary search tree.

6. **If Condition**: Inside the loop, if the value of `root` is less than or equal to the value of `x`, the method moves to the right subtree by setting `root` to `root->right`. This is because all values in the right subtree are larger than the value at `root`, and we're looking for a value larger than `x`.

7. **Else Condition**: If the value of `root` is greater than the value of `x`, the method sets `successor` to `root` and moves to the left subtree by setting `root` to `root->left`. This is because `root` is a potential successor (it's larger than `x`), but there may be a smaller value in the left subtree that is still larger than `x`.

8. **Return Statement**: After the loop, the method returns `successor`, which points to the in-order successor of `x` or `NULL` if `x` has no in-order successor.

## Time and Space Complexity:
### `Time Complexity`:
The time complexity of the code is O(h), where h is the height of the tree. This is because in the worst case, the method may need to traverse from the root to the deepest leaf node.

### `Space Complexity`:
The space complexity of the code is O(1), as no additional space is used that scales with the input size. The space used is constant, regardless of the size of the binary search tree.

## Code:
```cpp
/* The structure of Node
struct Node {
    int data;
    Node *left;
    Node *right;

    Node(int val) {
        data = val;
        left = right = NULL;
    }
};
*/

// The Solution class contains the logic for finding the inorder successor of a given Node in a Binary Search Tree (BST).
class Solution {
public:
    // Function to find the inorder successor of the Node x in BST (rooted at 'root').
    Node *inOrderSuccessor(Node *root, Node *x) {
        Node *successor = NULL;  // Initialize the successor to NULL.

        // Traverse the BST while root is not NULL.
        while (root != NULL) {
            // If the data of the current root is less than or equal to the data of Node x, move to the right subtree.
            if (root->data <= x->data) {
                root = root->right;
            } 
            // If the data of the current root is greater than the data of Node x, update successor and move to the left subtree.
            else {
                successor = root;
                root = root->left;
            }
        }

        // Return the found successor.
        return successor;
    }
};
```
