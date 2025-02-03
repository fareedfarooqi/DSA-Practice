# Climbing Stairs (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Climbing Stairs**](https://leetcode.com/problems/climbing-stairs/description/)

---

## Problem Description:

You are climbing a staircase. It takes `n` steps to reach the top.  
Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

### **Example 1**:

**Input**:  
`n = 2`  
**Output**:  
`2`  
**Explanation**: There are two ways to climb to the top.

1. 1 step + 1 step
2. 2 steps

### **Example 2**:

**Input**:  
`n = 3`  
**Output**:  
`3`  
**Explanation**: There are three ways to climb to the top.

1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step

## Constraints:

1 <= n <= 45

## Approach & Algorithm

### Solution: Recursive & Utilising Dynamic Programming

- Key in this question is to notice that it is built upon the Fibonacci Sequence.
- I have implemented a recursive solution that takes advantage of dynamic programming.
- I have used a memoized solution, whereby I am storing values that have been computed before. This is determined by the `memo` array's index. Initally all values at each index in the `memo` array are sent to `None`.
- If the value has been computed previously it will be stored at `memo[n]` and we can simply return that value as opposed to computing it again (which increases time complexity).
- If the value hasn't been computed previously, i.e., `memo[] = None`, then we simply compute the value `result = self.memoizedSol(n - 1, memo) + self.memoizedSol(n - 2, memo)` and store it back in `memo[n]`.

## Code Implementation

### Solution:

- **Time Complexity:** O(n)

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        # We create an array that is of length n and sent to None initially
        self.memo = [None] * (n + 1)
        return self.memoizedSol(n, self.memo)

    def memoizedSol(self, n: int, memo: []):
        result = None

        if memo[n] is not None:
            return memo[n]
        elif n == 1:
            result = 1
        elif n == 2:
            result = 2
        else:
            result = self.memoizedSol(n - 1, memo) + self.memoizedSol(n - 2, memo)

        memo[n] = result
        return result
```
