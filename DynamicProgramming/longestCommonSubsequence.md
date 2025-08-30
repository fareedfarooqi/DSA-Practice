# Longest Common Subsequence (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**1143. Longest Common Subsequence**](https://leetcode.com/problems/longest-common-subsequence/)

---

## **Problem Statement**

Given two strings `text1` and `text2`, return the **length** of their **longest common subsequence**.  

If there is **no common subsequence**, return `0`.

A **subsequence** of a string is a new string generated from the original string by **deleting some characters (can be none) without changing the relative order** of the remaining characters.

For example, `"ace"` is a subsequence of `"abcde"`.

A **common subsequence** of two strings is a **subsequence that appears in both strings**.

---

## **Example 1**

**Input:**
```python
text1 = "abcde"
text2 = "ace"
```

**Output:**
```python
3
```

**Explanation:**
The longest common subsequence is `"ace"`, and its length is 3.

## **Example 2**

**Input:**
```python
text1 = "abc"
text2 = "abc"
```

**Output:**
```python
3
```

**Explanation:**
The longest common subsequence is `"abc"`, and its length is 3.

## **Example 3**

**Input:**
```python
text1 = "abc"
text2 = "def"
```

**Output:**
```python
0
```

**Explanation:**
There is no common subsequence, so the result is 0.

## Constraints

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 400`

---

## Approach & Algorithm

- I've utilised dynamic programming to solve this question. I've utilised a bottom-up approach in the solution.
- I have hand-written my working and provided them below. Please refer to the algorithm being used there to understand the solution.

## Code Implementation

### Solution One - (Bottom Up Approach):

- **Time Complexity:** O(n * m)
- **Space Complexity:** O(n * m)

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        # We need to create a 2D matrix that represents either text on each axis.
        dp = [[0 for j in range(len(text2) + 1)] for i in range(len(text1) + 1)]

        for i in range(len(text1) - 1, -1, -1):
            for j in range(len(text2) -1, -1, -1):
                if text1[i] == text2[j]:
                    # We have found matching characters.
                    dp[i][j] = 1 + dp[i + 1][j + 1]
                else:
                    # We have NOT found matching characters. So we must fill the square appropraitely.
                    dp[i][j] = max(dp[i][j + 1], dp[i + 1][j])

        return dp[0][0]
```

![IMG_3416](https://github.com/user-attachments/assets/39da5eef-182f-4f0f-bb70-00b79f2797e7)

![IMG_3419](https://github.com/user-attachments/assets/da2fbbf0-07a1-42b3-9084-935d5ac0ab41)

![IMG_3418](https://github.com/user-attachments/assets/1d111b67-cb63-4409-81e5-98ae481a3434)

![IMG_3415](https://github.com/user-attachments/assets/724c5d00-fac0-498b-86a7-1f5e5fb5002c)

![IMG_3417](https://github.com/user-attachments/assets/1bda3745-a989-4976-8dc7-037125ec9b5e)

![IMG_3422](https://github.com/user-attachments/assets/e520265b-1ec6-43b4-bbc3-35225035b1d6)

![IMG_3420](https://github.com/user-attachments/assets/3c5fe957-0c0d-412d-aabc-13c70efc93ec)

![IMG_3421](https://github.com/user-attachments/assets/113faf93-dda3-42e3-8c67-0fdfb8357595)

![IMG_3423](https://github.com/user-attachments/assets/95b4ac83-df0b-4f9c-9613-63b87aab2e78)

### Solution Two - (Slow & Inefficient):

- **Time Complexity:** O(2^(n * m))
- **Note:** Use this solution below in order to understand my solution three below.

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        # Imagine this as a 2D grid i.e.,
        #
        # |   | a | b | c | d | e |
        # | a |   |   |   |   |   |
        # | c |   |   |   |   |   |
        # | e |   |   |   |   |   |
        #
        # The first character matches ("a") we can compare the subsequence
        # "bcde" vs "ce" and continue. Now compare the character "b" vs "c"
        # we can see they don't match. So we have two choices we either compare
        # "cde" vs "ce" OR "bcde" vs "e". We can do this recursively and see
        # how many total matches we get.

        def dfs(row, col):
            if row == len(text2) or col == len(text1):
                # Border case.
                return 0
            
            if text2[row] == text1[col]:
                # We increment by one and go diagonally to compare next part
                # i.e., "bcde" vs "ce".
                return 1 + dfs(row + 1, col + 1)
            
            return max(dfs(row + 1, col), dfs(row, col + 1))
        
        return dfs(0, 0)
```

### Solution Three - (Faster: Top-Down Apprroach):

- **Time Complexity:** O(n * m)

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        # Imagine this as a 2D grid i.e.,
        #
        # |   | a | b | c | d | e |
        # | a |   |   |   |   |   |
        # | c |   |   |   |   |   |
        # | e |   |   |   |   |   |
        #
        # The first character matches ("a") we can compare the subsequence
        # "bcde" vs "ce" and continue. Now compare the character "b" vs "c"
        # we can see they don't match. So we have two choices we either compare
        # "cde" vs "ce" OR "bcde" vs "e". We can do this recursively and see
        # how many total matches we get.

        cache = [[-1] * len(text1) for i in range(len(text2))]

        def dfs(row, col):
            if row == len(text2) or col == len(text1):
                # Border case.
                return 0

            if cache[row][col] > -1:
                return cache[row][col]
            
            if text2[row] == text1[col]:
                # We increment by one and go diagonally to compare next part
                # i.e., "bcde" vs "ce".
                cache[row][col] = (1 + dfs(row + 1, col + 1))
                return cache[row][col]
            
            cache[row][col] = max(dfs(row + 1, col), dfs(row, col + 1))
            return cache[row][col]
        
        return dfs(0, 0)
```
