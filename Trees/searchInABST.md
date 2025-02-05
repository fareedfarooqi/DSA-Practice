# Search in a Binary Search Tree (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Search in a Binary Search Tree**](https://leetcode.com/problems/search-in-a-binary-search-tree/)

---

## Problem Description

You are given the **root** of a **binary search tree (BST)** and an integer `val`.

Find the **node** in the BST whose value equals `val` and return the **subtree** rooted at that node. If such a node does not exist, return `null`.

---

## Examples

### **Example 1**

**Input:**

```python
root = [4,2,7,1,3], val = 2
```

**Output**:

```python
[2,1,3]
```

### **Example 2**

**Input:**

```python
root = [4,2,7,1,3], val = 5
```

**Output**:

```python
[]
```

## Constraints

- The number of nodes in the tree is in the range **[1, 5000]**.
- `1 <= Node.val <= 10^7`
- `root` is a **binary search tree**.
- `1 <= val <= 10^7`

---

## Approach & Algorithm

- This question required searching a Binary Tree.
- I utilised a recursive implementation whereby I check if the `val` is less than, greater than or equal to the `root.val`. Depending upon this I then carry out the appropriate action such as searching in the left or right sub-trees, or if we have found the value I return the `root`.
- If we have traversed the whole tree and we have not found a value that matches `val` we then simply return `None` (NULL).

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
    def searchBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
        if not root:
            return None

        if val < root.val:
            # Must be in the left sub-tree.
            return self.searchBST(root.left, val)
        elif val > root.val:
            # Must be in the right sub-tree.
            return self.searchBST(root.right, val)
        else:
            # Otherwise we are at the node with the correct value.
            return root
```
