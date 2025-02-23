# Minimum Depth of Binary Tree (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Minimum Depth of Binary Tree**](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

---

## Problem Statement

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the **shortest path** from the root node down to the nearest **leaf node**.

> **Note:** A leaf is a node with **no children**.

---

## **Example 1**

![Screenshot 2025-02-22 at 10 09 33 PM](https://github.com/user-attachments/assets/84dab0ac-eda8-4c4c-af3a-709e7cec771a)

**Input:**

```python
root = [3,9,20,null,null,15,7]
```

**Output:**

```python
2
```

## **Example 2**

**Input:**

```python
root = [2,null,3,null,4,null,5,null,6]
```

**Output:**

```python
5
```

## Constraints

- The number of nodes in the tree is in the range `[0, 10⁵]`.
- `1000 <= Node.val <= 1000`.

---

## Approach & Algorithm

- The trick to solving this question was to utilise a **Breadth-First-Search** (BFS) carefully.
- I also incorporated the use of a queue (a double-ended queue in particular).
- I done level-order traversal in both solutions.
  - In the first solution I also kept a `depth` set which simply added the current depth level in the tree once we reached a child node during traversal. I would then simply return the minimum value in this set.
  - In the second solution, I simply return the `minDepth` as soon as we reach a child node as opposed to creating a set. This reduces the overall computations we need to perform.

## Code Implementation

### Solution One - Using a Set (A little slower):

- **Time Complexity:** O(n).

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque

class Solution:
    def minDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0

        queue = deque()

        if root:
            queue.append(root)

        level = 0
        depth = set()
        while len(queue) > 0:
            for i in range(len(queue)):
                cur = queue.popleft()

                if not cur.left and not cur.right:
                    depth.add(level)

                if cur.left:
                    queue.append(cur.left)
                if cur.right:
                    queue.append(cur.right)

            level += 1

        return min(depth) + 1
```

### Solution Two - Returning at First Leaf Node:

- **Time Complexity:** O(n).

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque

class Solution:
    def minDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0

        queue = deque()

        if root:
            queue.append(root)

        level = 0
        depth = set()
        while len(queue) > 0:
            for i in range(len(queue)):
                cur = queue.popleft()

                if not cur.left and not cur.right:
                    depth.add(level)

                if cur.left:
                    queue.append(cur.left)
                if cur.right:
                    queue.append(cur.right)

            level += 1

        return min(depth) + 1
```
