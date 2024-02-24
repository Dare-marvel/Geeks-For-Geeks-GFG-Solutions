### [Insert a node in a BST](https://www.geeksforgeeks.org/problems/insert-a-node-in-a-bst/1?utm_source=geeksforgeeks&utm_medium=ml_article_practice_tab&utm_campaign=article_practice_tab)

## [Explanation](https://www.log2base2.com/data-structures/tree/insert-a-node-in-binary-search-tree.html)
1. **Struct Node**: This is a basic structure for a node in a binary search tree (BST). Each node contains an integer value (`data`), and two pointers (`left` and `right`) pointing to its left child and right child respectively. If a node does not have a left or right child, the corresponding pointer is `NULL`.

2. **Class Solution**: This class contains the method `insert` which is used to insert a new node into the BST.

3. **Method insert**: This method takes two arguments - a pointer to the root node of the BST (`node`), and the data of the new node to be inserted (`data`). The method returns a pointer to the root node of the BST after the insertion.

4. **Insertion Logic**: The method first checks if the BST is empty (i.e., `node == NULL`). If it is, it creates a new node with the given data and returns a pointer to this new node. If the BST is not empty, it starts from the root node and traverses the BST to find the correct position for the new node.

5. **Traversal**: The method uses a `while(true)` loop for traversal. Inside the loop, it compares the data of the new node with the data of the current node (`curr`). If the new data is greater than the current data, it goes to the right subtree; if less, it goes to the left subtree. If the new data is equal to the current data, it breaks the loop without inserting the new node (assuming the BST does not allow duplicate values).

6. **Insertion**: When the method finds the correct position for the new node (i.e., `curr->right` or `curr->left` is `NULL`), it creates a new node with the given data, links it as the right or left child of the current node, and breaks the loop.

7. **Return Value**: After the insertion, the method returns a pointer to the root node of the BST. Note that the root node does not change during the insertion, so it is the same as the input `node`.

## Time and Space Complexity:
### `Time Complexity`:
The time complexity of the `insert` method is O(h), where h is the height of the BST. This is because in the worst case, the method needs to traverse from the root to the deepest leaf node.The time complexity can become O(n) in the worst case scenario where the BST degenerates into a linked list (i.e., every node has only one child). This can happen if the input data is sorted, causing all new nodes to be inserted as the right child of the deepest node. To avoid this worst case scenario, a self-balancing BST could be used.

### `Space Complexity`:
The space complexity of the `insert` method is O(1), because it uses a constant amount of space to store the pointers `node` and `curr`, regardless of the size of the BST.

## Code:
```cpp
/*
    Define a Node structure to represent a binary tree node with an integer value,
    left and right child pointers.
*/
struct Node {
    int data;       // Data of the node
    Node* left;     // Pointer to the left child
    Node* right;    // Pointer to the right child

    // Constructor to initialize Node with a given value
    Node(int val) {
        data = val;
        left = right = NULL;
    }
};

/*
    Define a class Solution that provides a method for inserting a new node with a given
    value into a binary search tree.

    The binary search tree is constructed such that for each node, all elements in its left
    subtree are less than the node's value, and all elements in its right subtree are greater.

    The insert method iteratively inserts a new node into the binary search tree.
*/
class Solution {
public:
    // Function to insert a new node with the given data into the binary search tree
    Node* insert(Node* node, int data) {
        // If the tree is empty, create a new node with the given data
        if (node == NULL) return new Node(data);

        // Start from the root of the tree
        Node* curr = node;

        // Iterate until the correct position for the new node is found
        while (true) {
            // If the new data is greater than the current node's data
            if (data > curr->data) {
                // If there is a right child, move to the right child
                if (curr->right != NULL) {
                    curr = curr->right;
                } else {
                    // If no right child, insert the new node as the right child
                    curr->right = new Node(data);
                    break;  // Exit the loop after insertion
                }
            }
            // If the new data is less than the current node's data
            else if (data < curr->data) {
                // If there is a left child, move to the left child
                if (curr->left != NULL) {
                    curr = curr->left;
                } else {
                    // If no left child, insert the new node as the left child
                    curr->left = new Node(data);
                    break;  // Exit the loop after insertion
                }
            }
            // If the new data is equal to the current node's data, do not insert (BST property)
            else {
                break;  // Exit the loop without insertion
            }
        }

        return node;  // Return the root of the updated tree
    }
};

```
