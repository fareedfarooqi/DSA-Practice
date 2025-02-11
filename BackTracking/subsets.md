# Subsets (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Subsets**](https://leetcode.com/problems/subsets/)

---

## Problem Description

Given an integer array `nums` of **unique elements**, return **all possible subsets** (the power set).

The solution set **must not contain duplicate subsets**.  
Return the solution in **any order**.

---

## Examples

### **Example 1**

**Input:**

```python
nums = [1,2,3]
```

**Output:**

```
[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

### **Example 2**

**Input:**

```python
nums = [0]
```

**Output:**

```
[[],[0]]
```

## Constraints

- **`1 <= nums.length <= 10`**
- **`-10 <= nums[i] <= 10`**
- **All the numbers in `nums` are unique.**

---

## Approach & Algorithm

- I utilised backtracking (brute force method) of DFS to solve this problem.
- The key to solving this question was to understand that at each point we have the choice **to include a number** or **NOT** to include a number. As such we have `2^n` choices at each index whilst going through the array.
- We can break up this strategy and make it into a decision tree as shown in the example below. We will traverse each branch in our approach in order to get all possible subsets.

## Code Implementation

### Solution (DFS):

- **Time Complexity:** O(2^n)

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = []

        subset = []
        def dfs(index):
            if index >= len(nums):
                res.append(subset.copy())
                return

            # Decision to include nums[index]
            subset.append(nums[index])
            dfs(index + 1)

            # Decision to NOT include nums[index]
            subset.pop()
            dfs(index + 1)

        dfs(0)
        return res
```
