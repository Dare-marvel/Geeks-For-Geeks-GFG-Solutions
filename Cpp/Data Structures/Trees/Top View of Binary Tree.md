### [Top View of Binary Tree](https://www.geeksforgeeks.org/problems/top-view-of-binary-tree/1)

## Explanation:
Sure, here's an explanation of the code:

1. **Struct Node**: This is a definition for a binary tree node. Each node contains an integer value, and pointers to its left and right children.

2. **Class Solution**: This class contains the method `topView` which returns a list of nodes visible from the top view from left to right in a Binary Tree.

3. **Function topView**: This function takes the root of a binary tree as input and returns a vector containing the top view of the tree.

4. **Vector ans**: This vector stores the nodes visible from the top view of the tree.

5. **Map mpp**: This map stores the first node at each horizontal distance. The key is the horizontal distance and the value is the node's data.

6. **Queue q**: This queue is used to perform level-order traversal. It stores pairs of a node and its horizontal distance from the root.

7. **While loop**: This loop traverses the tree using level-order traversal. For each node, if it is the first node at its horizontal distance, it adds the node's data to the map. It then enqueues the left and right children with their respective horizontal distances.

8. **Adding node data to map**: If the node is the first node at its horizontal distance, its data is added to the map.

9. **Enqueue left and right children**: The left child is enqueued with a decreased horizontal distance. The right child is enqueued with an increased horizontal distance.

10. **Prepare the final result**: The final result is prepared by adding the data of the nodes in the map to the vector.

11. **Return the result**: The function returns the result, which is a vector containing the top view of the tree.

## Time and Space Complexity:
### `Time Complexity`:
The **time complexity** of the code is **O(N)**, where N is the number of nodes in the tree. This is because each node is processed once in the level-order traversal.

### `Space Complexity`:
The **space complexity** is also **O(N)**, as in the worst case, we might end up storing all the nodes in the queue (when the binary tree is a complete binary tree). Additionally, we also store all nodes in the map. Therefore, the space complexity is linear in the number of nodes.

## Code:
```cpp
/*
    Given a binary tree, this program aims to find and return a list of nodes visible from the top view
    in a left-to-right order.

    The algorithm uses a map to keep track of the nodes at each line (vertical position) in the top view.
    A queue is employed for level-order traversal, where each node is associated with its corresponding line.

    Algorithm Steps:
    1. Initialize an empty vector to store the top view nodes.
    2. Check if the tree is empty; if so, return an empty vector.
    3. Create a map 'mpp' to store nodes based on their lines.
    4. Create a queue 'q' and enqueue the root node with line 0.
    5. While the queue is not empty, dequeue a node and its associated line.
    6. If the line is not in 'mpp', add the node's data to 'mpp' at the current line.
    7. Enqueue the left child with a decremented line and the right child with an incremented line.
    8. Traverse 'mpp' and push the nodes into the result vector.
    9. Return the final result vector.

    This implementation ensures the top view nodes are organized and returned correctly.
*/

/*
struct Node
{
    int data;
    Node* left;
    Node* right;
};
*/

class Solution
{
public:
    // Function to return a list of nodes visible from the top view 
    // from left to right in Binary Tree.
    vector<int> topView(Node *root)
    {
        // Vector to store the top view nodes
        vector<int> ans;
        if (root == NULL)
            return ans;

        // Map to store nodes based on their lines
        map<int, int> mpp;

        // Queue for level-order traversal
        queue<pair<Node*, int>> q;
        q.push({root, 0});

        // Level-order traversal
        while (!q.empty())
        {
            auto it = q.front();
            q.pop();

            Node* node = it.first;
            int line = it.second;

            // If the line is not in 'mpp', add the node's data to 'mpp' at the current line.
            if (mpp.find(line) == mpp.end())
                mpp[line] = node->data;

            // Enqueue left child with decremented line and right child with incremented line.
            if (node->left)
                q.push({node->left, line - 1});
            if (node->right)
                q.push({node->right, line + 1});
        }

        // Traverse 'mpp' and push nodes into the result vector.
        for (auto it : mpp)
        {
            ans.push_back(it.second);
        }

        // Return the final result vector.
        return ans;
    }
};

```
