# Guess Number Higher or Lower (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Guess Number Higher or Lower**](https://leetcode.com/problems/guess-number-higher-or-lower/)

---

## Problem Description

We are playing the **Guess Game**. The game is as follows:

- I pick a number from `1` to `n`. You have to guess which number I picked.
- Every time you guess wrong, I will tell you whether the number I picked is **higher** or **lower** than your guess.

You call a pre-defined API:

```python
int guess(int num)
```

- `-1`: Your guess is higher than the number I picked (i.e. `num > pick`).
- `1`: Your guess is lower than the number I picked (i.e. `num < pick`).
- `0`: Your guess is equal to the number I picked (i.e. `num == pick`).

Return the number that I picked.

---

## Examples

### Example 1:

**Input**:
`Input: n = 10, pick = 6`

**Output**:
`Output: 6`

### Example 2:

**Input**:
`Input: n = 1, pick = 1`

**Output**:
`Output: 1`

### Example 3:

**Input**:
`Input: n = 2, pick = 1`

**Output**:
`Output: 1`

## Constraints

- `1 <= n <= 2^31 - 1`
- `1 <= pick <= n`

---

## Approach & Algorithm

- The key to completing this question was to notice that this question relies on the **binary search algorithm**.
- We need to search between the range of `1` and `n` for the `pick`.
- We utilise three pointers, `leftPtr`, `rightPtr` and `mid`. We loop until `leftPtr` is greater than `rightPtr` at which point we then know that the `pick` is **NOT** in range of `1` to `n` and as such we return `-1`. Otherwise, we have found `pick` in our range of `1` to `n` and we can return `mid`.
- We shift `leftPtr` and `rightPtr` accordingly to narrow down our search space.

## Code Solutions

- **Time Complexity**: It is `O(log(n))`.

```python
# The guess API is already defined for you.
# @param num, your guess
# @return -1 if num is higher than the picked number
#          1 if num is lower than the picked number
#          otherwise return 0
# def guess(num: int) -> int:

class Solution:
    def guessNumber(self, n: int) -> int:
        leftPtr, rightPtr, mid = 0, n, -1

        # Narrow down the search space
        while leftPtr <= rightPtr:
            mid = (leftPtr + rightPtr) // 2

            if guess(mid) == -1:
                rightPtr = mid - 1
            elif guess(mid) == 1:
                leftPtr = mid + 1
            else:
                return mid

        return -1
```
