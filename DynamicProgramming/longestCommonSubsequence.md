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

### Solution:

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

