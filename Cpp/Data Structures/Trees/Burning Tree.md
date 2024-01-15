### [Burning Tree](https://www.geeksforgeeks.org/problems/burning-tree/1)

## Explanation:
Sure, here's an explanation of the code:

1. **Struct Node**: This is a structure for a binary tree node. It contains an integer `data`, and two pointers `left` and `right` to point to the left and right child of the node respectively.

2. **Class Solution**: This class contains the main logic of the program. It has three public methods: `findMinTime`, `bfsToParents`, and `minTime`.

3. **Method findMinTime**: This method takes a target node and a map (which maps each node to its parent) as input. It performs a breadth-first search (BFS) starting from the target node. The BFS traverses not only the child nodes but also the parent node (which is stored in the map). The method returns the maximum depth it can reach, which is the minimum time to burn the binary tree from the target node.

4. **Method bfsToParents**: This method performs a standard BFS starting from the root node. During the BFS, it builds a map that maps each node to its parent. It also finds the target node during the BFS. The method returns the target node.

5. **Method minTime**: This is the main method that is called with the root of the binary tree and the target data. It first calls `bfsToParents` to get the target node and the map (node to parent mapping). Then it calls `findMinTime` with the target node and the map as input to get the minimum time to burn the tree.

## Time and Space Complexity:
### `Time Complexity`:
The time complexity of the code is **O(n)**, where **n** is the number of nodes in the binary tree. This is because each node is processed once in the BFS.

### `Space Complexity`:
The space complexity of the code is also **O(n)**. The space is mainly used to store the queue in the BFS and the map (node to parent mapping). In the worst case, all nodes will be stored in the queue and the map, so the space complexity is **O(n)**.

## Code:
```cpp
/*
   The given C++ code defines a class Solution that contains functions to find the minimum time required 
   to reach a target node in a binary tree from its root using BFS (Breadth-First Search).
*/

#include <iostream>
#include <queue>
#include <map>

struct Node {
    int data;
    Node *left;
    Node *right;

    Node(int val) {
        data = val;
        left = right = nullptr;
    }
};

class Solution {
public:
    // Function to find the minimum time using BFS
    int findMinTime(Node* target, std::map<Node*, Node*>& mpp) {
        std::queue<Node*> q;
        q.push(target);
        std::map<Node*, int> vis;
        vis[target] = 1;
        int maxi = 0;

        while (!q.empty()) {
            int size = q.size();
            int fl = 0;

            for (int i = 0; i < size; i++) {
                auto curr = q.front();
                q.pop();
                
                // Check and traverse left child
                if (curr->left && !vis[curr->left]) {
                    fl = 1;
                    vis[curr->left] = 1;
                    q.push(curr->left);
                }

                // Check and traverse right child
                if (curr->right && !vis[curr->right]) {
                    fl = 1;
                    vis[curr->right] = 1;
                    q.push(curr->right);
                }

                // Check and traverse parent
                if (mpp[curr] && !vis[mpp[curr]]) {
                    fl = 1;
                    vis[mpp[curr]] = 1;
                    q.push(mpp[curr]);
                }
            }
            if (fl) maxi++;
        }

        return maxi;
    }

    // Function to perform BFS and track parents
    Node* bfsToParents(Node* root, std::map<Node*, Node*>& mpp, int target) {
        std::queue<Node*> q;
        q.push(root);
        Node* res;

        while (!q.empty()) {
            Node* curr = q.front();
            q.pop();
            
            // Track the target node
            if (curr->data == target) 
                res = curr;

            // Track and traverse left child
            if (curr->left) {
                mpp[curr->left] = curr;
                q.push(curr->left);
            }

            // Track and traverse right child
            if (curr->right) {
                mpp[curr->right] = curr;
                q.push(curr->right);
            }
        }
        return res;
    }

    // Function to find the minimum time from root to target node
    int minTime(Node* root, int target) {
        std::map<Node*, Node*> mpp;
        Node* tar = bfsToParents(root, mpp, target);
        return findMinTime(tar, mpp);
    }
};
```
