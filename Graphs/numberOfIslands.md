# Number of Islands (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Number of Islands**](https://leetcode.com/problems/number-of-islands/)

---

## Problem Statement

Given an `m x n` 2D binary grid `grid` which represents a map of **'1'** (land) and **'0'** (water), return the **number of islands**.

An island is surrounded by water and is formed by connecting adjacent lands **horizontally or vertically**. You may assume all four edges of the grid are surrounded by water.

---

## **Example 1**

**Input:**

```python
grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
```

**Output:**

```python
1
```

## **Example 2**

**Input:**

```python
grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
```

**Output:**

```python
3
```

## Constraints

- The number of nodes in the tree is in the range `[0, 10⁵]`.
- `1000 <= Node.val <= 1000`.

---

## Approach & Algorithm

- I utilised a traditional Matrix DFS algorithm with backtracking to solve this problem.
- The only twist to solving the problem was to keep a `count` variable which kept track of how many islands we have come across.
- I run a loop in order to go through the `grid`, everytime I notice that `grid[i][j] == '1'`, we know that we have found the start of an island. So we call our helper function `_dfs()`, to run a recursive matrix DFS. This DFS algorithm will set every `grid[row][col]` that is currently `'1'` to `'0'` in order to mark that this part of the island is visited and we can move on until the entire island has been visited in which case the DFS has completed running for that particular island. We then continue with our loop to find the next starting island indicated by a `'1'` in the `grid`.

## Code Implementation

### Solution:

- **Time Complexity:** O(N \* M).

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        count = 0
        for i in range(len(grid)):
            for j in range(len(grid[i])):
                if grid[i][j] == '1':
                    count += 1
                    self._dfs(grid, count, i, j, set())
        return count

    def _dfs(self, grid: List[List[str]], count, row, col, visited):
        ROWS, COLS = len(grid), len(grid[0])

        if (min(row, col) < 0 or row == ROWS or col == COLS or (row, col) in visited
            or grid[row][col] == '0'):
            return
        if grid[row][col] == '1':
            grid[row][col] = '0'

        visited.add((row, col))

        self._dfs(grid, count, row + 1, col, visited)
        self._dfs(grid, count, row - 1, col, visited)
        self._dfs(grid, count, row, col + 1, visited)
        self._dfs(grid, count, row, col - 1, visited)

        visited.remove((row, col))
```
