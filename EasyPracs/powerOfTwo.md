# Power of Two (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Power of Two**](https://leetcode.com/problems/power-of-two/)

---

## Problem Statement

Given an integer `n`, return `true` if it is a power of two. Otherwise, return `false`.

An integer `n` is a power of two if there exists an integer `x` such that:

\[
n = 2^x
\]

---

## **Example 1**

**Input:**

```python
n = 1
```

**Output:**

```python
True
```

**Explanation:**

- `2^0 = 1`

## **Example 2**

**Input:**

```python
n = 16
```

**Output:**

```python
True
```

**Explanation:**

- `2^4 = 16`

## **Example 3**

**Input:**

```python
n = 3
```

**Output:**

```python
False
```

**Explanation:**

- `3 is not a power of 2.`

## Constraints

- The number of nodes in the tree is in the range `[0, 10⁵]`.
- `1000 <= Node.val <= 1000`.

---

## Approach & Algorithm

- If a number `n` is divided by `2` repeatedly until we get `n <= 1` we can then see if `n == 1` or not. If `n == 1` then it is a power of `2`, otherwise it is not a power of `2`.
- There is a way to do this using bitwise operations. I would like to explore that.

## Code Implementation

### Solution:

- **Time Complexity:** O(log(n)).

```python
class Solution:
    def isPowerOfTwo(self, n: int) -> bool:
        # If a number is divided by two repeatedly and we take it to it's
        # lowest possible form i.e., if after repeated division by two
        # we get '1', then we know that 'n' is a power of 2.

        while n > 1:
            n = n / 2

        return True if n == 1 else False
```
