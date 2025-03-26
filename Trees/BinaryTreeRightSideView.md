# Binary Tree Right Side View (Medium)

---

## 🔗 LeetCode Link:

Here is the link to the problem on LeetCode:  
[**Binary Tree Right Side View**](https://leetcode.com/problems/binary-tree-right-side-view/)

---

## Problem Description

Given the `root` of a binary tree, imagine yourself standing on the **right side** of it.

Return the values of the nodes you can **see**, ordered from **top to bottom**.

---

## Examples

### **Example 1**

![Screenshot 2025-02-10 at 11 55 25 AM](https://github.com/user-attachments/assets/fae2572e-272b-40c6-b60a-0e1489813724)

**Input:**

```python
root = [1,2,3,null,5,null,4]
```

**Output:**

```python
[1,3,4]
```

### **Example 2**

![Screenshot 2025-02-10 at 11 55 40 AM](https://github.com/user-attachments/assets/70dae89f-c7ec-4de8-9b78-6d6eed120d6e)

**Input:**

```python
root = [1,2,3,4,null,null,null,5]
```

**Output:**

```python
[1,3,4,5]
```

### **Example 3**

**Input:**

```python
root = [1,null,3]
```

**Output:**

```python
[1,3]
```

### **Example 4**

**Input:**

```python
root = []
```

**Output:**

```python
[]
```

## 🔎 Constraints

- The number of nodes in the tree is in the range **`[0, 100]`**.
- **`-100 <= Node.val <= 100`**.

---

## Approach & Algorithm

- My approach to this question was to utilise the **Breadth-First-Search** algorithm.
- My thoughts to do this was due to the fact that the question requires us to only return a list of right-most nodes. So, we need to essentially do a level-by-level processing of the nodes.
- I utilised a double-ended `queue`, an array `rightChildren` and another array `childrenAtCurrentLevel`. The key to this problem were the two arrays.
  - The `childrenAtCurrentLevel` array allowed me to add all the children at the current level so we can keep track of them.
  - The `rightChildren` array allowed me to take the rightmost child from `childrenAtCurrentLevel` array and track it. I processed each level and at the end of each level (second loop), I checked if the length of `childrenAtCurrentLevel` was greater than 0, if it was I simply appended the last element from `childrenAtCurrentLevel` into `rightChildren`.

## Code Implementation

### Solution (BFS):

- **Time Complexity:** O(n)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque

class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        queue = deque()
        rightChildren = []

        if root:
            queue.append(root)
            rightChildren.append(root.val)

        while len(queue) > 0:
            childrenAtCurrentLevel = []

            for i in range(len(queue)):
                cur = queue.popleft()

                if cur.left and not cur.right:
                    queue.append(cur.left)
                    childrenAtCurrentLevel.append(cur.left.val)
                elif cur.left:
                    queue.append(cur.left)
                    childrenAtCurrentLevel.append(cur.left.val)
                if cur.right:
                    queue.append(cur.right)
                    childrenAtCurrentLevel.append(cur.right.val)

            if len(childrenAtCurrentLevel) > 0:
                rightChildren.append(childrenAtCurrentLevel[len(childrenAtCurrentLevel) - 1])

        return rightChildren
```
