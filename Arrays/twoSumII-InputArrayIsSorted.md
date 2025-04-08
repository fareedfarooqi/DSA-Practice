# Two Sum II - Input Array Is Sorted (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**167. Two Sum II - Input Array Is Sorted**](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

---

## Problem Statement

Given a 1-indexed array of integers `numbers` that is already **sorted in non-decreasing order**, find two numbers such that they add up to a specific `target` number.  
Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`.

Return the indices of the two numbers, `index1` and `index2`, **added by one** as an integer array `[index1, index2]` of length 2.

- The tests are generated such that **there is exactly one solution**.
- You **may not use the same element twice**.
- Your solution must use **only constant extra space**.

---

## Example 1

**Input:**

```python
numbers = [2,7,11,15]
target = 9
```

**Output:**

```python
[1,2]
```

**Explanation:**

```plaintext
The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2.
```

## Example 2

**Input:**

```python
numbers = [2,3,4]
target = 6
```

**Output:**

```python
[1,3]
```

**Explanation:**

```plaintext
The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3.
```

## Example 3

**Input:**

```python
numbers = [-1,0]
target = -1
```

**Output:**

```python
[1,2]
```

**Explanation:**

```plaintext
The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2.
```

---

## Constraints:

- `2 <= numbers.length <= 3 * 10⁴`
- `1000 <= numbers[i] <= 1000`
- `numbers` is sorted in **non-decreasing** order
- `1000 <= target <= 1000`
- The tests are generated such that **there is exactly one solution**

---

## Approach & Algorithm

-

## Code Implementation:

### Solution One:

- **Time Complexity:** `O(n)`

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        L, R = 0, len(numbers) - 1

        while L < R:
            loopTotal = numbers[L] + numbers[R]

            if loopTotal > target:
                # Our total is greater than the target as such we must bring the right pointer down.
                R -= 1
            elif loopTotal < target:
                # Our total is less than the target so we must move the left pointer up.
                L += 1
            else:
                # The total of our loop adds up to the target.
                return [L + 1, R + 1]
```
