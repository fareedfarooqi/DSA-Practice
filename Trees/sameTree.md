# Same Tree (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**100. Same Tree**](https://leetcode.com/problems/same-tree/)

---

## **Problem Statement**

Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

Two binary trees are considered the same if:
- They are **structurally identical**
- The **nodes have the same values**

---

## **Example 1**

**Input:**
```python
p = [1, 2, 3]
q = [1, 2, 3]
```

**Output:**
```
true
```

## **Example 2**

**Input:**
```python
p = [1, 2]
q = [1, null, 2]
```

**Output:**
```
false
```

## **Example 3**

**Input:**
```python
p = [1, 2, 1]
q = [1, 1, 2]
```

**Output:**
```
false
```

---

## **Constraints**

- The number of nodes in both trees is in the range `[0, 100]`
- `10⁴ <= Node.val <= 10⁴`

---

## Approach & Algorithm:

- The approach to solving this question was to realise it required a modified BFS traversal of the tree.
- I have two double-ended queues - `pQueue` and `qQueue` to which we append the root node initially and then the children of tree `p` and `q` respectively.
- We carry out the BFS traversal, however, I have an additional data structure `pLevelElems` and `qLevelElems` that are dictionaries. As we go through the traversal, I also add each child to it's respective dictionary. The **key** is the literal value of the child node and the **value** a string that states whether this node was a "left" or "right" child.
- After traversing each level we compare the dictionaries, if they are not equal we know that the two trees are not equal and hence we return `False`, otherwise we return `True`.

## Code Implementation:

### Solution:

- **Time Complexity:** `O(n)` - We need to traverse each node in the tree.

```python
from collections import deque

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        pQueue = deque()
        qQueue = deque()

        if p and q:
            pQueue.append(p)
            qQueue.append(q)
        elif p == q:
            return True
        else:
            return False

        # Check if the root nodes are not equal.
        if p.val != q.val:
            return False
        
        while len(pQueue) > 0 and len(qQueue) > 0:
            pLevelElems = {}
            qLevelElems = {}

            for i in range(len(pQueue)):
                pCur = pQueue.popleft()

                if pCur.left:
                    # Add left child of pQueue
                    pQueue.append(pCur.left)
                    pLevelElems[pCur.left.val] = "left"
                
                if pCur.right:
                    pQueue.append(pCur.right)
                    pLevelElems[pCur.right.val] = "right"

            for i in range(len(qQueue)):
                qCur = qQueue.popleft()

                if qCur.left:
                    # Add left child of pQueue
                    qQueue.append(qCur.left)
                    qLevelElems[qCur.left.val] = "left"

                if qCur.right:
                    qQueue.append(qCur.right)
                    qLevelElems[qCur.right.val] = "right"

            if pLevelElems != qLevelElems:
                return False
    
        return True
```