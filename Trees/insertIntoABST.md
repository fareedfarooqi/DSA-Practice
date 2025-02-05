# Insert into a Binary Search Tree (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Insert into a Binary Search Tree**](https://leetcode.com/problems/insert-into-a-binary-search-tree/)

---

## Problem Description

You are given the **root node** of a **binary search tree (BST)** and a value `val` to insert into the tree. Return the **root node** of the BST after the insertion.

It is **guaranteed** that the new value **does not exist** in the original BST.

There may exist **multiple valid ways** for the insertion, as long as the tree **remains a BST** after insertion. You can return **any valid BST**.

---

## Examples

### **Example 1**

**Input:**

```python
root = [4,2,7,1,3], val = 5
```

**Output**:

```python
[4,2,7,1,3,5]
```

### **Example 2**

**Input:**

```python
root = [40,20,60,10,30,50,70], val = 25
```

**Output**:

```python
[40,20,60,10,30,50,70,null,null,25]
```

### **Example 3**

**Input:**

```python
root = [4,2,7,1,3,null,null,null,null,null,null], val = 5
```

**Output**:

```python
[4,2,7,1,3,5]
```

## Constraints

- The number of nodes in the tree will be in the range **[0, 10⁴]**.
- `-10⁸ <= Node.val <= 10⁸`
- All the values `Node.val` are **unique**.
- `-10⁸ <= val <= 10⁸`
- It is **guaranteed** that `val` **does not exist** in the original BST.

---

## Approach & Algorithm

- We use the standard method of inserting at the leaf node to solve this problem.
- We recursively traverse down the tree depending upon whether `root.val > val` or `root.val < val`.
  - If `root.val > val` it means that the value of the current root is bigger than the value we would like to insert, therefore we must search the left sub-tree.
  - If `root.val < val` it means that the value of the current root is smaller than the value we would like to insert, therefore we must search the right sub-tree.
- Once we have reached a point where we are at NULL (`None`), we can simply create a new node and insert it with the `val`. We then return that new node.
- After returning from the first recursive call, we are reassigning what `root.left` or `root.right` points to. They simply point to the newly inserted node.

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
    def insertIntoBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
        # If we are at NULL insert the node.
        if not root:
            return TreeNode(val)

        if root.val > val:
            # Go into left sub-tree.
            root.left = self.insertIntoBST(root.left, val)
        elif root.val < val:
            # Go into the right sub-tree.
            root.right = self.insertIntoBST(root.right, val)

        return root
```
