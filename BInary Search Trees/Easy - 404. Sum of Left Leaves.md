### 404. The sum of Left Leaves

Given the root of a binary tree, return the sum of all left leaves.

A leaf is a node with no children. A left leaf is a leaf that is the left child of another node.

![image](https://github.com/swethamurthy25/My-LeetCode/assets/112581595/282f3d5d-e62f-473e-b45b-31d3cc78db6b)

_______________________________________________________

### General Understanding:
1. Navigate through the binary tree from the top (root) until the last leaf.
2. Sum all the left leaves alone and return as output
3. We can achieve this using the Depth-first traversal method
________________________________________________________________________________

### Approach 1: Recursion - https://www.youtube.com/watch?v=TEKLUJftP5M

1. If the root node is None, meaning the tree is empty or the current subtree has reached its end, the method returns 0.
2. Then the condition checks if there is a left node; If the left node exists it further checks whether the
   left & right sides of the left node are None: Then returns the root.left.val
3. And also it recursively calls sumOfLeftLeaves on the right subtree (root.right).
4. This ensures that if there are more nodes to the right of the current subtree, their left leaves will also be considered.
5. If the root node is not a leaf node or doesn't meet the condition to be considered a left leaf, the method recursively
   calculates the sum of left leaves for both the left subtree (root.left) and the right subtree (root.right).
6. The sum of these values is returned.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:
        if root is None: 
            return 0
        if root.left and root.left.left is None and root.left.right is None:
            return root.left.val + self.sumOfLeftLeaves(root.right)
        return self.sumOfLeftLeaves(root.left) + self.sumOfLeftLeaves(root.right)
```
TC is O(N) Where N is the number of nodes in the binary tree.
SC is O(N) 
_____________________________________________________________________________________________________

### Approach 2: DFS - [https://www.youtube.com/watch?v=TEKLUJftP5M](https://www.youtube.com/watch?v=Ti9wPXqbT8Q)

1. Initialize self.sum to store the sum of left leaf values.
2. def dfs(root): Defines a nested function dfs for depth-first search traversal of the binary tree.
3. if the root is None:: Base case. If the current node root is None, the function returns 0.
4. if root.left:: it further checks whether the left & right nodes of the left are none.
5. If it's true, it's the leaf node, so the value is added to the sum.
6. dfs(root.left): Recursively calls the dfs function on the left child of the current node root.
7. dfs(root.right): Recursively calls the dfs function on the right child of the current node .
8. Again dfs(root): Initiates the depth-first search traversal starting from the root node root.
9. return self.sum: Returns the sum of left leaf values stored in self.sum.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:
        self.sum = 0
        def dfs(root):
            if root is None:
                return 0
            if root.left:
                if root.left.left == None and root.left.right == None:
                    self.sum += root.left.val
            dfs(root.left)
            dfs(root.right)
        dfs(root)
        return self.sum
```
TC is O(N) and SC is O(N)
