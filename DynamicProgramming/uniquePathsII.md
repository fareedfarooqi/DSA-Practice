# Unique Paths II (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**63. Unique Paths II**](https://leetcode.com/problems/unique-paths-ii/)

---

## **Problem Statement**

You are given an `m x n` integer array `obstacleGrid`.  

- A **robot** is initially located at the **top-left corner** (i.e., `grid[0][0]`).
- The robot **tries to move to the bottom-right corner** (i.e., `grid[m - 1][n - 1]`).
- The robot can **only move either down or right** at any point in time.

An **obstacle** is marked as `1`, and an **empty space** is marked as `0`.  
A path that the robot takes **cannot include any square that is an obstacle**.

Return the **number of possible unique paths** that the robot can take to reach the **bottom-right corner**.

The test cases are generated so that the answer will be **≤ 2 * 10⁹**.

---

## **Example 1**

**Input:**
```python
obstacleGrid = [[0,0,0],
                [0,1,0],
                [0,0,0]]
```

**Output:**
# Unique Paths II (Medium)


---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**63. Unique Paths II**](https://leetcode.com/problems/unique-paths-ii/)

---

## **Problem Statement**

You are given an `m x n` integer array `obstacleGrid`.  

- A **robot** is initially located at the **top-left corner** (i.e., `grid[0][0]`).
- The robot **tries to move to the bottom-right corner** (i.e., `grid[m - 1][n - 1]`).
- The robot can **only move either down or right** at any point in time.

An **obstacle** is marked as `1`, and an **empty space** is marked as `0`.  
A path that the robot takes **cannot include any square that is an obstacle**.

Return the **number of possible unique paths** that the robot can take to reach the **bottom-right corner**.

The test cases are generated so that the answer will be **≤ 2 * 10⁹**.

---

## **Example 1**

![1](https://github.com/user-attachments/assets/60b288c7-9e2e-402f-b3a3-775b62b06b99)

**Input:**
```python
obstacleGrid = [[0,0,0],
                [0,1,0],
                [0,0,0]]
```

**Output:**
```python
2
```

**Explanation:**
There is one obstacle in the middle of the `3x3` grid.
There are two ways to reach the bottom-right corner:

1. `Right -> Right -> Down -> Down`
2. `Down -> Down -> Right -> Right`
   
![IMG_3412](https://github.com/user-attachments/assets/73e40b2d-c67e-48cb-83a9-e68668c2e6bd)

## **Example 2**

![2](https://github.com/user-attachments/assets/30b4ad56-2f53-49f1-b739-4220e5f6baa1)

**Input:**
```python
obstacleGrid = [[0,1],
                [0,0]]
```

**Output:**
```python
1
```

## Constraints

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 400`

---

## Approach & Algorithm

- I've utilised dynamic programming to solve this question. I've utilised a bottom-up approach in Solution One.
- In particular I have used a single list `dp` to keep track of the number of paths from a square for that given row. I've set the last square in `dp` to be `1` to indicate the that there is only one way to reach the destination for the destination itself.
  - `dp = [0, 0, 1]` initially.
- I loop thorugh in reverse order starting from the final square in the last row. We build our way back up.
- This code takes a while to understand. Refer to diagrams attached above and carry out the algorithm physically on an example.

## Code Implementation:

### Solution:

- **Time Complexity:** O(n * m)
- **Space Complexity:** O(n)

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        M, N = len(obstacleGrid), len(obstacleGrid[0])
        dp = [0] * len(obstacleGrid[0])
        dp[N - 1] = 1

        for r in reversed(range(M)):
            for c in reversed(range(N)):
                if obstacleGrid[r][c] == 1:
                    # The square is BLOCKED.
                    dp[c] = 0
                elif c + 1 < N:
                    dp[c] = dp[c] + dp[c + 1]

        return dp[0]
```
