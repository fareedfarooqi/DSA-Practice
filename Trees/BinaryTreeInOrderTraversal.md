# Binary Tree Inorder Traversal (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Binary Tree Inorder Traversal**](https://leetcode.com/problems/binary-tree-inorder-traversal/)

---

## Problem Description

Given the `root` of a binary tree, return the **inorder traversal** of its nodes' values.

---

## Examples

### **Example 1**

**Input:**

```python
root = [1,null,2,3]
```

**Output**:

```python
[1,3,2]
```

### **Example 2**

**Input:**

```python
root = [1,2,3,4,5,null,8,null,null,6,7,9]
```

**Output**:

```python
[4,2,6,5,7,1,3,9,8]
```

### **Example 3**

**Input:**

```python
root = []
```

**Output**:

```python
[]
```

### **Example 4**

**Input:**

```python
root = [1]
```

**Output**:

```python
[1]
```

## Constraints

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

---

## Approach & Algorithm

- This question involved utilising **in-order traversal** for a binary tree using the **depth-first search** algorithm.
- We start at the root node and traverse as far down left as we can, we append the leaf node (in left sub-tree) to our `arr`. We then go back to the leaf node's parent node.
- We then append the parent node to `arr`.
- After processing the parent node, we traverse down to it's right sub-tree (going as far and left in the sub-tree as we can), we append it's value to `arr`. If the right sub-tree only has one value we simply append that to `arr` and go back to the parent's parent node.
- We have a helper function `_dfs()` that helps us perform a DFS.

## Code Implementation

### Solution:

- **Time Complexity:** O(n)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        arr = []
        return self._dfs(root, arr)

    # Our helper function
    def _dfs(self, root: Optional[TreeNode], arr: List[int]) -> List[int]:
        if not root:
            return arr

        self._dfs(root.left, arr)
        arr.append(root.val)
        self._dfs(root.right, arr)
        return arr
```
