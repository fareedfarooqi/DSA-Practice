# Max Area of Island (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Max Area of Island**](https://leetcode.com/problems/max-area-of-island/)

---

## Problem Statement

You are given an `m x n` binary matrix `grid`. An **island** is a group of **'1'**s (**land**) connected **4-directionally** (horizontal or vertical). You may assume all four edges of the grid are surrounded by **water**.

The **area** of an island is the **number of '1' cells** in that island.

Return the **maximum area** of an island in `grid`. If there is no island, return `0`.

---

## **Example 1**

<img width="621" alt="Screenshot 2025-02-25 at 10 25 38 PM" src="https://github.com/user-attachments/assets/f0af389f-5566-4421-bdaf-2c6e03686347" />

**Input:**

```python
grid = [
  [0,0,1,0,0,0,0,1,0,0,0,0,0],
  [0,0,0,0,0,0,0,1,1,1,0,0,0],
  [0,1,1,0,1,0,0,0,0,0,0,0,0],
  [0,1,0,0,1,1,0,0,1,0,1,0,0],
  [0,1,0,0,1,1,0,0,1,1,1,0,0],
  [0,0,0,0,0,0,0,0,0,0,1,0,0],
  [0,0,0,0,0,0,0,1,1,1,0,0,0],
  [0,0,0,0,0,0,0,1,1,0,0,0,0]
]
```

**Output:**

```python
6
```

**Explanation:**

```plaintext
The answer is not 11, because the island must be connected 4-directionally.
```

## **Example 2**

**Input:**

```python
grid = [[0,0,0,0,0,0,0,0]]
```

**Output:**

```python
0
```

## Constraints

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 50`
- `grid[i][j] is either 0 or 1.`

---

## Approach & Algorithm

- I utilised a Matrix DFS (with backtracking) to solve this question.
- This question has somewhat of a similar approach to the `numberOfIslands` question.
- I looped through the entire matrix:
  - If I found a `grid[i][j]` whereby it equaled `1`, I knew that we have found an island and I enter the depth-first search. Otherwise if it is `0` we know we have hit water so we can continue with the loop.
  - I passed in an `area` list has lists preserve their values when passed across functions unlike regular integers. But the key here was that I only used one space to store the area of the island `area[0]`.
  - I also utilised a `visited` set in order to keep track of the areas in the matrix we have already been to during the depth-first search.
  - The rest of the algorithm was pretty straight-forward as is standard with a matrix DFS.

## Code Implementation

### Solution:

- **Time Complexity:** O(N \* M).

```python
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        max_area = 0
        for i in range(len(grid)):
            for j in range(len(grid[i])):
                if grid[i][j] == 1:
                    area = [0]
                    area_of_island = self._dfs(grid, i, j, set(), area)

                    if area_of_island > max_area:
                        max_area = area_of_island

        return max_area

    def _dfs(self, grid: List[List[int]], row, col, visited, area) -> int:
        ROWS, COLS = len(grid), len(grid[0])

        if (min(row, col) < 0 or row == ROWS or col == COLS
            or (row, col) in visited or grid[row][col] == 0):
            return area[0]

        if (grid[row][col] == 1):
            cur_area = area.pop() + 1
            area.append(cur_area)
            grid[row][col] = 0

        visited.add((row, col))

        self._dfs(grid, row + 1, col, visited, area)
        self._dfs(grid, row - 1, col, visited, area)
        self._dfs(grid, row, col + 1, visited, area)
        self._dfs(grid, row, col - 1, visited, area)

        visited.remove((row, col))
        return area[0]
```
