# Delete Node in a BST (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Delete Node in a BST**](https://leetcode.com/problems/delete-node-in-a-bst/)

---

## Problem Description

Given a **root node reference** of a **Binary Search Tree (BST)** and a `key`, delete the node with the given `key` in the BST. Return the **root node reference** (possibly updated) of the BST.

The deletion can be divided into two stages:

1. **Search** for the node to remove.
2. If the node is found, **delete the node**.

---

## Examples

### **Example 1**

**Input:**

```python
root = [5,3,6,2,4,null,7], key = 3
```

**Output**:

```python
[5,4,6,2,null,null,7]

```

### **Example 2**

**Input:**

```python
root = [5,3,6,2,4,null,7], key = 0
```

**Output**:

```python
[5,3,6,2,4,null,7]
```

### **Example 3**

**Input:**

```python
root = [], key = 0
```

**Output**:

```python
[]
```

## Constraints

- The number of nodes in the tree is in the range `[0, 10^4]`.
- `-10^5 <= Node.val <= 10^5`
- Each node has a **unique value**.
- `root` is a valid **binary search tree**.
- `-10^5 <= key <= 10^5`

---

## Approach & Algorithm

- This question required that I search the binary tree for the `key`, if it exists I do further checks before deleting the node.
  - The node to be deleted could have `0` or `1` child. If this is the case we can simply return either `root.left` or `root.right`. They either point to a valid child or `NULL` (`None`), which means that the node to be deleted will be replaced by the child or `NULL`.
  - The node to be deleted could have `2` children. If this is the case we replace the node to be deleted by the smallest node in the node to be deleted's right sub-tree. I have created a function `findMin()` which serves this exact purpose.
- The accordingly we reassign the right or left pointers after the recursive calls.

## Code Implementation

### Solution:

- **Time Complexity:** O(log(n))

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def deleteNode(self, root: Optional[TreeNode], key: int) -> Optional[TreeNode]:
        if not root:
            # Node does NOT exist.
            return None

        if root.val > key:
            root.left = self.deleteNode(root.left, key)
        elif root.val < key:
            root.right = self.deleteNode(root.right, key)
        else:
            # Now we must check how many nodes are attached to
            # the node we are about to delete.
            if not root.left:
                return root.right
            elif not root.right:
                return root.left
            else:
                # We have two children nodes. We must return
                # the smallest node in the right-subtree.
                smallest_node = self.findMin(root.right)
                root.val = smallest_node.val
                # Now we need to remove the smallest node as we
                # have moved it up to replace the deleted node.
                root.right = self.deleteNode(root.right, root.val)

        return root

    def findMin(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        cur = root

        while cur and cur.left:
            cur = cur.left

        return cur
```
