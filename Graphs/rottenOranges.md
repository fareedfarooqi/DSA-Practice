# Rotting Oranges (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**994. Rotting Oranges**](https://leetcode.com/problems/rotting-oranges/)

---

## Problem Statement

You are given an `m x n` grid where each cell can have one of three values:

- `0` representing an empty cell,
- `1` representing a fresh orange, or
- `2` representing a rotten orange.

Every minute, any fresh orange that is **4-directionally adjacent** to a rotten orange becomes rotten.

Return the **minimum number of minutes** that must elapse until no cell has a fresh orange.  
If this is **impossible**, return `-1`.

---

## **Example 1**

**Input:**

```python
grid = [
  [2,1,1],
  [1,1,0],
  [0,1,1]
]
```

**Output:**
```python
4
```

## **Example 2**

**Input:**

```python
grid = [
  [2,1,1],
  [0,1,1],
  [1,0,1]
]
```

**Output:**
```python
-1
```

**Explanation:**
```plaintext
The orange in the bottom left corner `(row 2, column 0)` is never rotten,
because rotting only happens 4-directionally.
```

## **Example 3**

**Input:**

```python
grid = [[0,2]]
```

**Output:**
```python
0
```

**Explanation:**
```plaintext
Since there are already no fresh oranges at minute 0, the answer is just 0.
```

## Constraints

- `n == grid.length`
- `n == grid[i].length`
- `1 <= n <= 100`
- `grid[i][j] is 0 or 1.`

---

## Approach & Algorithm

- I have utilised a Matrix BFS to solve this question.
- The key to answering this question was to realise that rotten oranges **DO NOT** necessarily always have to start from index `[0, 0]`. In fact there can be more than 1 rotten orange to begin with and they can all be located all over the grid.
- So we can utilise a `visited` set and a double-ended `queue` to keep track of nodes we have visited as well as the current nodes we need to traverse.
- We use a `level` variable which essentially just keeps track of minutes. Remember that we are doing level order traversal, so at each level we process `0` or more oranges may become affected and become rotten.
- There are some special checks such as to see if the grid contains all zeros which would indicate that no oranges are present in the grid so we can simply return `0`. There are also other checks such as to see after our main algorithm has run to see whether there are any fresh oranges `1`'s remaining in the grid. If there are it would mean that not all oranges are affected and thus we return `-1` (Orange may be in a corner separated from the remaining oranges). 

## Code Implementation

### Solution:

- **Time Complexity:** O(m x n).

```python
from collections import deque

class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        ROWS, COLS = len(grid), len(grid[0])
        visited = set()
        queue = deque()
        level = 0

        # If grid is 1x1 return special case.
        if len(grid) == 1 and len(grid[0]) == 1 and grid[0][0] == 0:
            return 0
        
        # We must locate all rotten oranges first and add them to the queue. Find all "2's".
        allZeros = True
        for i in range(ROWS):
            for j in range(COLS):
                # Rotten orange found. Added it to visited and queue.
                if grid[i][j] == 1:
                    allZeros = False
                elif grid[i][j] == 2:
                    visited.add((i, j))
                    queue.append((i, j))
                    allZeros = False

        if allZeros:
            return 0

        while queue:
            for i in range(len(queue)):
                row, col = queue.popleft()
                
                # Make it rotten.
                if grid[row][col] == 1:
                    grid[row][col] = 2
                
                neighbours = [[0, 1], [0, -1], [1, 0], [-1, 0]]

                for dr, dc in neighbours:
                    newRow, newCol = row + dr, col + dc

                    if (min(newRow, newCol) < 0 or newRow == ROWS or newCol == COLS
                        or grid[newRow][newCol] == 0 or (newRow, newCol) in visited):
                        continue
                    
                    # Otherwise we have found a fresh ('1') orange. 
                    visited.add((newRow, newCol))
                    queue.append((newRow, newCol))

            level += 1

        for i in range(ROWS):
            for j in range(COLS):
                if grid[i][j] == 1:
                    # Means we have a orange that is not affected. Maybe far away.
                    return -1

        return level - 1
```