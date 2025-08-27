# Combination Sum (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Combination Sum**](https://leetcode.com/problems/combination-sum/)

---

## Problem Description

Given an array of **distinct** integers `candidates` and a target integer `target`, return a list of all **unique combinations** of `candidates` where the chosen numbers sum to `target`.

You may return the combinations **in any order**.

- The **same number** may be chosen from `candidates` **an unlimited number of times**.
- Two combinations are **unique** if the **frequency** of at least one of the chosen numbers is different.
- The test cases are generated such that the number of unique combinations that sum up to `target` is **less than 150** combinations.

---

## Examples

### **Example 1**

**Input:**

```python
candidates = [2,3,6,7]
target = 7
```

**Output::**

```python
[[2,2,3],[7]]
```

**Explanation:**

- `2` and `3` are candidates, and `2 + 2 + 3 = 7`.
- `7` is a candidate, and `7 = 7`.
- These are the only two valid combinations.

### **Example 2**

**Input:**

```python
candidates = [2,3,5]
target = 8
```

**Output::**

```python
[[2,2,2,2],[2,3,3],[3,5]]
```

### **Example 3**

**Input:**

```python
candidates = [2]
target = 1
```

**Output::**

```python
[]
```

## Constraints

- **`1 <= candidates.length <= 30`**
- **`2 <= candidates[i] <= 40`**
- **All elements of `candidates` are distinct.**
- **`1 <= target <= 40`**

---

## Approach & Algorithm

- I utilised **backtracking** in combination with **Depth-First-Search** algorithm to solve this question.
- The key to solving this question was to understand it's recusive nature.
- I've utilised two lists - `res` (for our final lists of lists that we return) and `setList` which is used to find the invidual list that sums to `target`.
- We have 3 main conditions:
  - `if index >= len(candidates)`, means if at any point during our recursion our index is greater than the length of the candidates then we know we have gone too deep and must track back up.
  - `if sum(setList) == target`, means if the sum of our `setList` is equal to our `target` then we know we have found a valid list of numbers as they sum to our target. We can then append it to our final `res` list and return (track back up).
  - `elif sum(setList) > target`, means that the current sum of our `setList` is greater than the `target`, so we know we have added the current value too many times to our `setList` or the number we added to `setList` is simply greater than the `target` (with our without adding it to previous elements in `setList`). We must then remove it from our `setList` after being returned and trackback up.
- We also append the number from candidates (based on the current index), and then perform our DFS.

## Code Implementation

### Solution One:

- **Time Complexity:** O(2^t*t)
- **Note:** Slower because of the linear complexity of the sum function.

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []
        setList = []

        def dfs(index):
            if index >= len(candidates):
                return

            if sum(setList) == target:
                res.append(setList.copy())
                return
            elif sum(setList) > target:
                return

            setList.append(candidates[index])
            dfs(index)
            index += 1
            setList.pop()
            dfs(index)
            return

        dfs(0)
        return res
```

### Solution Two - (A Bit Faster)

- **Time Complexity:** O(2^t)

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        result = []
        sumList = []
        sumOfSumList = 0

        def dfs(i):
            nonlocal sumOfSumList
            if i >= len(candidates):
                if sumOfSumList == target:
                    result.append(sumList.copy())
                return
            elif sumOfSumList > target:
                return

            sumList.append(candidates[i])
            sumOfSumList += candidates[i]
            dfs(i)

            sumList.pop()
            sumOfSumList -= candidates[i]
            dfs(i + 1)

        dfs(0)

        return result
```
