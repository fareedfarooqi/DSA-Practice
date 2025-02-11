# Path Sum (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Path Sum**](https://leetcode.com/problems/path-sum/)

---

## Problem Description

Given the `root` of a binary tree and an integer `targetSum`, return `true` if the tree has a **root-to-leaf path** such that adding up all the values along the path equals `targetSum`.

A **leaf** is a node with no children.

---

## Examples

### **Example 1**

**Input:**

```python
root = [5,4,8,11,null,13,4,7,2,null,null,null,1]
targetSum = 22
```

**Output:**

```python
true
```

**Explanation:**
The root-to-leaf path with the target sum is shown in the tree.

### **Example 2**

**Input:**

```python
root = [5,4,8,11,null,13,4,7,2,null,null,null,1]
targetSum = 22
```

**Output:**

```python
false
```

**Explanation:**
There are two root-to-leaf paths in the tree:

- `(1 --> 2)`: The sum is `3`.
- `(1 --> 3)`: The sum is `4`.

There is no root-to-leaf path with sum `5`.

### **Example 3**

**Input:**

```python
root = []
targetSum = 0
```

**Output:**

```python
false
```

**Explanation:**
Since the tree is empty, there are no root-to-leaf paths.

## Constraints

- The number of nodes in the tree is in the range **`[0, 5000]`**.
- **`-1000 <= Node.val <= 1000`**.
- **`-1000 <= targetSum <= 1000`**.

---

## Approach & Algorithm

- I utilised a variant of DFS to solve this backtracking problem.
- The key in this question was to subtract the `root.val` from `targetSum` given that we are not at `NULL`.
- This is a brute force approach whereby we go down every valid path and see if our `targetSum` by the time we reach the leaf node is `0`.
  - If it is `0` we have found a valid path that sums to `targetSum`.
  - If it is not `0` we have not found a valid path.

## Code Implementation

### Solution (DFS):

- **Time Complexity:** O(n)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        # We are at NULL - we have NOT found a path that sums to targetSum.
        if not root:
            return False

        targetSum -= root.val

        # Another base case: we are at leaf node.
        if not root.left and not root.right and targetSum == 0:
            return True

        return self.hasPathSum(root.left, targetSum) or self.hasPathSum(root.right, targetSum)
```
