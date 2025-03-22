# 338. Counting Bits (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**338. Counting Bits**](https://leetcode.com/problems/counting-bits/)

---

## **Problem Statement**

Given an integer `n`, return an array `ans` of length `n + 1` such that for each `i` (`0 <= i <= n`), `ans[i]` is the number of `1`s in the **binary representation** of `i`.

---

## **Example 1**

**Input:**
```python
n = 2
```

**Output:**
```python
[0, 1, 1]
```

**Explanation:**
- `0` → `0` → `0` one
- `1` → `1` → `1` one
- `2` → `10` → `1` one

## **Example 2**

**Input:**
```python
n = 5
```

**Output:**
```python
[0, 1, 1, 2, 1, 2]
```

**Explanation:**
- `0` → `0` → `0` one
- `1` → `1` → `1` one
- `2` → `10` → `1` one
- `3` → `11` → `2` ones
- `4` → `100` → `1` one
- `5` → `101` → `2` ones

## Constraints

- `0 <= n <= 10⁵`

---

## Approach & Algorithm:

- Both solutions use bit manipulation in order to solve the problem. However, solution one utilises dynamic programming so we will focus on that (it is faster).
- The trick is to realise there is a lot of recomputed work being done which can be cached and used again as opposed to recomputing a value.
- For example, if we have numbers 0 to 8, the numbers 0 to 3 will have the same final 2 bits as the numbers 4 to 7 (difference of 4 --> so number 4 has 1 bit more than number 0, number 3 has 1 more bit than number 1, etc). So we can simply count the number of bits in that manner (refer to the diagram for a more visual understanding). We will have an `offset` that essentially keeps track of the most significant bit of the number we are on.

## Code Implementation

### Solution One (FAST):

- **Time Complexity:** `O(n)`

```python
class Solution:
    def countBits(self, n: int) -> List[int]:
        dp = [0] * (n + 1)
        offset = 1

        for i in range(1, n + 1):
            if offset * 2 == i:
                offset = i

            dp[i] = 1 + dp[i - offset]
        
        return dp
```

### Solution Two (SLOW):

- **Time Complexity:** `O(n * log(n))`

```python
class Solution:
    def countBits(self, n: int) -> List[int]:
        counts = []
        
        for i in range(n + 1):
            count = 0
            while i > 0:
                if i & 1 == 1:
                    count += 1
                
                i = i >> 1
            counts.append(count)
        
        return counts
```