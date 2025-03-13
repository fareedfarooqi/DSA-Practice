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

- This question could have been solved in multiple ways. I've provided 3 solutions (2 are working). This question was built on top of the Fibonacci Sequence.
- We need to incorporate the use of dynamic programming to solve this question in a timely manner otherwise we get TLE (Time Limit Exceeded) with certain test cases.
- **Solution One** incorporates the use of memoization (caching) to store the results of computation in a hash map. We store a solution **once** we see it the first time, i.e., if we need to compute the 3rd Fibonnaci number a second time we can simply grab it's value from the cache (we stored it in the cache after our first computation). This also has a linear space complexity.
- **Sequence Two** incorporates the use of a bottom-up approach. It has the same time complexity as the previous solution however this has a constant space complexity. We start from the first node (1) and build up to `n`. We must recall that Fibonacci sequence is simply the sum of the two predecessor numbers i.e., `F(n) = F(n - 1) + F(n - 2)`. Our array `dp` simply stores the `n - 1` and `n - 2` numbers and we replace them appropriately each time we compute something.

## Code Implementation

### Solution One (Fast - Using Memoization (Caching) --> Top-Down Approach):

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        return self.memoization(n, {})

    def memoization(self, n, cache):
        if n <= 2:
            return n
        elif n in cache:
            return cache[n]

        cache[n] = self.memoization(n - 1, cache) + self.memoization(n - 2, cache)
        return cache[n]
```

### Solution Two (Fast -- Using Bottom-Up Approach):

- **Time Complexity:** O(n)
- **Time Complexity:** O(1)

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n <= 2:
            return n

        dp = [0, 1]
        i = 1

        while i <= n:
            tmp = dp[1]
            dp[1] = dp[1] + dp[0]
            dp[0] = tmp
            i += 1

        return dp[1]
```

### Solution Three (TLE - Too Slow):

- **Time Complexity:** O(2^n)

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n <= 2:
            return n

        return self.climbStairs(n - 1) + self.climbStairs(n - 2)
```
