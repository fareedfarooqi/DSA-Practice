# Kth Smallest Element in a BST (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Kth Smallest Element in a BST**](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

---

## **Problem Description**

Given the `root` of a **binary search tree (BST)** and an integer `k`, return the **k-th smallest value** (1-indexed) among all the node values in the tree.

---

## **Examples**

### **Example 1**

**Input:**

```python
root = [3,1,4,null,2]
k = 1
```

**Output:**

```python
1
```

### **Example 2**

**Input:**

```python
root = [5,3,6,2,4,null,null,1]
k = 3
```

**Output:**

```python
3
```

## Constraints

- The number of nodes in the tree is `n`.
- `1 <= k <= n <= 10^4`
- `0 <= Node.val <= 10^4`

---

## Approach & Algorithm

- I have utilised the **depth-first search** algorithm with **in-order** traversal to complete this problem.
- The key idea here is to manage state in someway. I have provided two solutions whereby one solution utilises a `dict` and the other solution utilises a `list`.
- The key idea here is to understand that we are managing state using two variables.
  - In either solution we have some sort of `nodeVisitedCount` variable that increments how many nodes we have visited from the bottom up. So we traverse all the way down to the smallest node, i.e., imagine we have nodes 1 to 5. We traverse down to 1, after which we then begin counting the nodes we have visited. So, visiting node 1 would result in `nodeVisitedCount += 1`, now `nodeVisitedCount = 1`. Then we go up to 2 we do the same thing`nodeVisitedCount += 1`, but now `nodeVisitedCount = 2`.
  - We also utilise some form of `valAtRoot` variable, that is set once `nodeVisitedCount == k`, meaning that we are at the desired `kth` element.

## Code Implementation

### Solution 1 (Inefficient - Dict):

- **Time Complexity:** O(n)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        myDict = { "nodeVisitedCount": 0, "valAtRoot": -1 }

        return self._DFS(root, k, myDict)

    def _DFS(self, root: Optional[TreeNode], k: int, myDict: {}) -> int:
        if not root:
            return

        self._DFS(root.left, k, myDict)
        myDict["nodeVisitedCount"] += 1
        if myDict["nodeVisitedCount"] == k:
            myDict["valAtRoot"] = root.val
        self._DFS(root.right, k, myDict)

        return myDict["valAtRoot"]
```

### Solution 2 (Faster - List Method):

- **Time Complexity:** O(n)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        state = [0, -1]
        self._DFS(root, k, state)
        return state[1]

    def _DFS(self, root: Optional[TreeNode], k: int, state: [int]) -> int:
        if not root:
            return

        self._DFS(root.left, k, state)

        state[0] += 1
        if state[0] == k:
            state[1] = root.val
            return

        self._DFS(root.right, k, state)

        return state[1]
```
