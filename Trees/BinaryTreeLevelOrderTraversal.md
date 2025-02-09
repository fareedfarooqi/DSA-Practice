# Binary Tree Level Order Traversal (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Binary Tree Level Order Traversal**](https://leetcode.com/problems/binary-tree-level-order-traversal/)

---

## Problem Description

Given the `root` of a binary tree, return the **level order traversal** of its nodes' values.  
(i.e., from left to right, level by level).

---

## Examples

### **Example 1**

![Screenshot 2025-02-09 at 12 17 19 PM](https://github.com/user-attachments/assets/1ee3f930-a77e-4f79-867c-ad235bef23d6)

**Input:**

```python
root = [3,9,20,null,null,15,7]
```

**Output:**

```python
[[3],[9,20],[15,7]]
```

### **Example 2**

**Input:**

```python
root = [1]
```

**Output:**

```python
[[1]]
```

### **Example 3**

**Input:**

```python
root = []
```

**Output:**

```python
[]
```

## 🔎 Constraints

- The number of nodes in the tree is in the range **`[0, 2000]`**.
- **`-1000 <= Node.val <= 1000`**.

---

## Approach & Algorithm

- I have utilised the breadth-first-search algorithm to solve this question.
- I have taken use of a double-ended queue and a list to solve this problem.
- My queue `queue` allowed me to take a first-in-first-out approach. I started from the root level and processed the node at each level. I checked in each level at each node if the node had children if it did they were added to the back of the queue.
- I processed each level, I checked if there were children and if there were children I appended them to our `nodesNext` list. I then appended the `nodesNext` list to our `returnList` only if `nodesNext` was not empty.

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
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        queue = deque()
        returnList = []

        if root:
            queue.append(root)
            returnList.append([root.val])

        while len(queue) > 0:
            nodesNext = []
            for i in range(len(queue)):
                cur = queue.popleft()

                if cur.left:
                    queue.append(cur.left)
                    nodesNext.append(cur.left.val)
                if cur.right:
                    queue.append(cur.right)
                    nodesNext.append(cur.right.val)

            if nodesNext:
                returnList.append(nodesNext)

        return returnList
```
