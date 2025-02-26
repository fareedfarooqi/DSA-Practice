# Shortest Path in Binary Matrix (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Shortest Path in Binary Matrix**](https://leetcode.com/problems/shortest-path-in-binary-matrix/)

---

## Problem Statement

Given an `n x n` binary matrix `grid`, return the **length of the shortest clear path** in the matrix. If there is no clear path, return `-1`.

A **clear path** in a binary matrix is a path from the **top-left cell** `(0,0)` to the **bottom-right cell** `(n-1, n-1)`, such that:

1. **All visited cells in the path are `0`**.
2. **All adjacent cells in the path are 8-directionally connected** (i.e., they share an edge or a corner).
3. **The length of a clear path is the number of visited cells**.

---

## **Example 1**

**Input:**

```python
grid = [[0,1],
        [1,0]]
```

**Output:**

```python
2
```

## **Example 2**

**Input:**

```python
grid = [[0,0,0],
        [1,1,0],
        [1,1,0]]
```

**Output:**

```python
4
```

## **Example 3**

**Input:**

```python
grid = [[1,0,0],
        [1,1,0],
        [1,1,0]]
```

**Output:**

```python
-1
```

**Explanation:**

```plaintext
The starting cell (0,0) is blocked (1), so no path is possible.
```

## Constraints

- `n == grid.length`
- `n == grid[i].length`
- `1 <= n <= 100`
- `grid[i][j] is 0 or 1.`

---

## Approach & Algorithm

- I utilised a Matrix BFS to solve this question.
- The major trick to this question was understanding that once we are at a node, we can move in **8** directions. These include:
  - Up
  - Bottom
  - Left
  - Right
  - Top-left diagonal
  - Top-right diagonal
  - Bottom-left diagonal
  - Bottom-right diagonal
- We go layer by layer -- node by node. We keep track of the current layer/level by utilising a `queue` (double-ended queue from the `collections` library).
- We also utilised a `visited` set to ensure we are not visiting the same nodes repeatedly.
-

## Code Implementation

### Solution One (Fatser):

- **Time Complexity:** O(n^2).

```python
from collections import deque

class Solution:
    def shortestPathBinaryMatrix(self, grid: List[List[int]]) -> int:
        ROWS, COLS = len(grid), len(grid[0])

        if (grid[0][0] == 1 or grid[ROWS - 1][COLS - 1] == 1):
            return -1

        length = 1
        visited = set()
        queue = deque()
        queue.append((0, 0))
        visited.add((0, 0))
        directions = [[0, 1], [0, -1], [1, 0], [-1, 0],
                    [-1, -1], [-1, 1], [1, -1], [1, 1]]

        while queue:
            for _ in range(len(queue)):
                curRow, curCol = queue.popleft()

                if curRow == ROWS - 1 and curCol == COLS - 1:
                    return length

                for dr, dc in directions:
                    newRow, newCol = curRow + dr, curCol + dc

                    if not (0 <= newRow < ROWS and 0 <= newCol < COLS and grid[newRow][newCol] == 0 and (newRow, newCol) not in visited):
                        continue

                    queue.append((newRow, newCol))
                    visited.add((newRow, newCol))

            length += 1

        return -1
```

### Solution Two (Slower - More Inefficient):

- **Time Complexity (Slower):** O(n^2).

```python
from collections import deque

class Solution:
    def shortestPathBinaryMatrix(self, grid: List[List[int]]) -> int:
        ROWS, COLS = len(grid), len(grid[0])

        if (grid[0][0] == 1 or grid[ROWS - 1][COLS - 1]):
            return -1

        visited = set()
        queue = deque()
        queue.append((0, 0))
        visited.add((0, 0))

        length = 1

        while queue:
            for i in range(len(queue)):
                curRow, curCol = queue.popleft()

                if curRow == ROWS - 1 and curCol == COLS - 1:
                    return length

                neighbours = [[0, 1], [0, -1], [1, 0], [-1, 0],
                                [-1, -1], [-1, 1], [1, -1], [1, 1]] # Inefficient as we just declare these over and over.

                for dr, dc in neighbours:
                    if (min(curRow + dr, curCol + dc) < 0 or curRow + dr == ROWS
                        or curCol + dc == COLS or (curRow + dr, curCol + dc) in visited or
                        grid[curRow + dr][curCol + dc] == 1):
                        continue
                    queue.append((curRow + dr, curCol + dc))
                    visited.add((curRow + dr, curCol + dc))

            length += 1

        return -1
```
