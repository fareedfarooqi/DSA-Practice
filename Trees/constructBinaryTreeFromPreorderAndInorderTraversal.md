# Construct Binary Tree from Preorder and Inorder Traversal (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Construct Binary Tree from Preorder and Inorder Traversal**](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

---

## Problem Description

Given two integer arrays `preorder` and `inorder` where:

- `preorder` represents the **preorder traversal** of a binary tree.
- `inorder` represents the **inorder traversal** of the same tree.

Construct and return the **binary tree**.

---

## Examples

### **Example 1**

![Screenshot 2025-02-08 at 3 08 55 PM](https://github.com/user-attachments/assets/7468f293-28ad-4fee-8d82-4a40ace344a6)

**Input:**

```python
preorder = [3,9,20,15,7]
inorder  = [9,3,15,20,7]
```

**Output:**
`[3,9,20,null,null,15,7]`

### **Example 1**

**Input:**

```python
preorder = [3,9,20,15,7]
inorder  = [9,3,15,20,7]
```

**Output:**

```python
[3,9,20,null,null,15,7]
```

### **Example 2**

**Input:**

```python
preorder = [3,9,20,15,7]
inorder  = [9,3,15,20,7]
```

**Output:**

```python
[3,9,20,null,null,15,7]
```

---

## Approach & Algorithm

- I will only discuss my Solution 2 approach as that works and is much faster.
- The key to solving this problem is to understand a few fundemental things.
  - The `preorder` list gives us our starting **root** node. The first element in this list will always be our root off of which we can build the node's left and right sub-trees.
  - The `inorder` list actually tells us the correct order of the nodes in the respective trees.
  - The `mid` variable gives us the index of the root node in the `inorder` list traversal. This is important because everything to the left off the root node in the `inorder` list belongs to the root node's left subtree. Everything to the right of the root node in the `inorder` traversal list belongs to it's right subtree. This can be said for the other nodes in the tree as well. We must utilise recursion.
- Take `preorder = [3,9,20,15,7]` and `inorder  = [9,3,15,20,7]`. Here, as per the solution we take a `root` which is `3` and a `mid`, which is at `index = 1` in our `inorder` list.
- Everything from `preorder[1:mid + 1]` belongs to the left sub-tree, so it is the left-node that connects to the root node i.e., `[9]`. Then, `preorder[mid + 1]` belongs to the right sub-tree i.e., `[20, 15, 7]`.
- Everything from `inorder[:mid]` belongs to the left of the root nodes sub-tree i.e., `[9]` and everything from `inorder[mid + 1:]` belongs to the root node's right sub-tree i.e., `[15,20,7]`.
- We then build the left and right sub-trees recursively.

## Code Implementation

### Solution 1 (Inefficient - Too Slow (Fails large test cases)):

- **Time Complexity:** O(n^2)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        # We are at the leaf node.
        if not preorder or not inorder:
            return None

        # Get the root node.
        root = preorder[0]
        root_node = TreeNode(root)
        root_inorder_index = inorder.index(root)

        left_inorder_subtree = inorder[:root_inorder_index]
        right_inorder_subtree = inorder[root_inorder_index + 1:]

        left_preorder_subtree = preorder[1:1 + len(left_inorder_subtree)]
        right_preorder_subtree = preorder[1 + len(left_inorder_subtree):]

        root_node.left = self.buildTree(left_preorder_subtree, left_inorder_subtree)
        root_node.right = self.buildTree(right_preorder_subtree, right_inorder_subtree)

        return root_node
```

### Solution 1 (Inefficient - Too Slow (Fails large test cases)):

- **Time Complexity:** O(n^2)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        # We are at the leaf node.
        if not preorder or not inorder:
            return None

        root = TreeNode(preorder[0])
        mid = inorder.index(preorder[0])

        # Now we construct the subtrees using splices.
        root.left = self.buildTree(preorder[1:mid + 1], inorder[:mid])
        root.right = self.buildTree(preorder[mid + 1:], inorder[mid + 1:])

        return root
```
