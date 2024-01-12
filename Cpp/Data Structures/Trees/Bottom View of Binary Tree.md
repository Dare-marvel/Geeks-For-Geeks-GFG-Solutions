### [Bottom View of Binary Tree](https://www.geeksforgeeks.org/problems/bottom-view-of-binary-tree/1)

## Explanation:
1. **Class Definition**: The code defines a class named `Solution` which contains a public method `bottomView`.

2. **Method Definition**: The `bottomView` method takes a pointer to a `Node` object as an argument and returns a vector of integers. This method is used to find the bottom view of a binary tree.

3. **Initial Checks**: If the root of the binary tree is `NULL`, an empty vector is returned as there are no nodes to process.

4. **Data Structures**: The method uses a map (`mpp`) to store the bottom-most node at each horizontal distance from the root node, and a queue (`q`) to perform a level order traversal of the binary tree.

5. **Queue Initialization**: The root node and its horizontal distance (0 in this case) are pushed into the queue as a pair.

6. **Traversal**: A while loop is used to traverse the binary tree. For each node, its data is stored in the map with its horizontal distance as the key. If the node has a left or right child, these children and their respective horizontal distances are pushed into the queue.

7. **Map Processing**: After the traversal, the map contains the bottom-most node at each horizontal distance. These nodes are pushed into the vector `ans` in order of their horizontal distance.

8. **Return Statement**: Finally, the vector `ans` is returned, which contains the bottom view of the binary tree.


## Time and Space Complexity:
### `Time Complexity`:
The **time complexity** of the code is **O(n)**, where **n** is the number of nodes in the binary tree. This is because each node is processed once in the level order traversal.

### `Space Complexity`:
The **space complexity** is also **O(n)**, due to the extra space required for the queue and the map. In the worst case, the queue might need to store all nodes of a level, and the map might need to store all nodes of the tree.

## Code:
```cpp
// Definition of a class named Solution
class Solution {
  public:
    // Function to find the bottom view of a binary tree
    vector <int> bottomView(Node *root) {
        // Vector to store the bottom view elements
        vector<int> ans;

        // Check if the root is NULL, return empty result
        if(root == NULL) return ans;

        // Map to store the horizontal distance and corresponding node value
        map<int, int> mpp;

        // Queue for level order traversal using a pair of Node pointer and horizontal distance
        queue<pair<Node*, int>> q;
        q.push({root, 0});

        // Loop until the queue is not empty
        while(!q.empty()){
            // Get the front element of the queue
            auto it = q.front();
            q.pop();
            
            // Extract the Node and its horizontal distance
            Node* node = it.first;
            int line = it.second;

            // Update the map with the latest value at the current horizontal distance
            mpp[line] = node->data;

            // If the left child exists, push it to the queue with a decreased horizontal distance
            if(node->left != NULL) q.push({node->left, line-1});

            // If the right child exists, push it to the queue with an increased horizontal distance
            if(node->right != NULL) q.push({node->right, line+1});
        }

        // Iterate through the map and store the values in the result vector
        for(auto it:mpp){
            ans.push_back(it.second);
        }

        // Return the bottom view of the binary tree
        return ans;
    }
};
```
