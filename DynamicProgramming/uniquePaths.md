# Unique Paths (Medium)

---

## 🔗 LeetCode Link:

Here is the link to the problem on LeetCode:  
[**62. Unique Paths**](https://leetcode.com/problems/unique-paths/)

---

## **Problem Statement**

There is a robot on an `m x n` grid. The robot is initially located at the **top-left corner** (i.e., `grid[0][0]`).  
The robot tries to move to the **bottom-right corner** (i.e., `grid[m - 1][n - 1]`).

The robot can **only move either down or right** at any point in time.

Given two integers `m` and `n`, return the **number of possible unique paths** that the robot can take to reach the bottom-right corner.

The test cases are generated so that the answer will be **≤ 2 \* 10⁹**.

---

## **Example 1**

**Input:**

```python
m = 3, n = 7
```

**Output:**

```python
28
```

![Screenshot 2025-03-15 at 9 56 54 PM](https://github.com/user-attachments/assets/7b204312-3280-4b0f-960a-ea784e15ab3e)

**My Approach:**
![IMG_3409 2](https://github.com/user-attachments/assets/733faa28-8909-4779-b501-f25aed977c4a)

## **Example 2**

**Input:**

```python
m = 3, n = 2
```

**Output:**

```python
3
```

**Explanation:**

```plaintext
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:

1. `Right -> Down -> Down`
2. `Down -> Down -> Right`
3. `Down -> Right -> Down`
```

## Constraints:

- `1 <= m, n <= 100`

## Approach & Algorithm

- This question required the use of dynamic programming in order to solve it in an efficient manner. There are two approaches I could have taken:
  - Top-Down Approach: Memoized Solution (need to look into this). Bad Space complexity as we will need to replicate a caching mechanism.
  - Bottom-Up Approach: Good space complexity.
- In solution one below, I've utilised a Bottom-Up Approach. Essentially I start from the very last square (set it to 1) and work out each row. It is important to note that the way to find the value (the number of ways to get to the end) from a particular square is by adding the number in the right square and the bottom square. This is why I've utilised a `prevRow` and `curRow` to help me keep track of rows. We only need two rows at a time to solve this particular problem so there is no need to cache/store an entire grid like we would have done with a top-down approach. We slowly work our way up from the last square of each row and move one column left at a time and find how many solutions for each and every sqaure in a particular row before moving to the row above the current row. Please view the diagrams above for a complete understanding.

## Code Implementation:

### Solution One (Fast: Bottom-Up Approach):

- **Time Complexity:** O(n \* m)
- **Space Complexity:** O(1)

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        prevRow = [0] * n

        for r in range(m - 1, -1, -1):
            curRow = [0] * n
            curRow[n - 1] = 1

            for c in range(n - 2, -1, -1):
                curRow[c] = curRow[c + 1] + prevRow[c]

            prevRow = curRow

        return curRow[0]
```

### Solution Two - (Fast: Top-Down Approach)

- **Time Complexity:** O(n \* m)
- **Space Complexity:** O(n \* m)

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        # Some cases to check include ensuring that the robot
        # is not out of bounds on the right-hand side as well
        # as ensure the robot is not out of bounds from the
        # bottom of the grid.
        
        row, col = 0, 0
        NUM_ROWS, NUM_COLS = m, n
        cache = [ [0] * n for i in range(m) ]
        
        def dfs(row, col, numPaths = 0):
            if row == NUM_ROWS or col == NUM_COLS:
                return 0
            
            if row == NUM_ROWS - 1 and col == NUM_COLS - 1:
                return 1

            # If we have already computed this return it from our cache.
            if cache[row][col] != 0:
                return cache[row][col]

            numPaths = 0
            # We can only move in two directions:
            # --- Move Down
            # --- Move Right
            numPaths += dfs(row + 1, col, numPaths)
            numPaths += dfs(row, col + 1, numPaths)
            cache[row][col] = numPaths

            return cache[row][col]
        
        return dfs(0, 0)
```

### Solution Three - (Slow & Inefficient)

- **Time Complexity:** O(2^(n + m)
- **Space Complexity:** O(1)

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        # Some cases to check include ensuring that the robot
        # is not out of bounds on the right-hand side as well
        # as ensure the robot is not out of bounds from the
        # bottom of the grid.
        
        row, col = 0, 0
        NUM_ROWS, NUM_COLS = m, n
        
        def dfs(row, col, numPaths = 0):
            if row == NUM_ROWS or col == NUM_COLS:
                return 0
            
            if row == NUM_ROWS - 1 and col == NUM_COLS - 1:
                return 1

            numPaths = 0
            # We can only move in two directions:
            # --- Move Down
            # --- Move Right
            numPaths += dfs(row + 1, col, numPaths)
            numPaths += dfs(row, col + 1, numPaths)

            return numPaths
        
        return dfs(0, 0)

