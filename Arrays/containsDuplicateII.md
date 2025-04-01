# Contains Duplicate II (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**219. Contains Duplicate II**](https://leetcode.com/problems/contains-duplicate-ii/)

---

## **Problem Statement**

Given an integer array `nums` and an integer `k`, return `true` if there are two distinct indices `i` and `j` in the array such that:

- `nums[i] == nums[j]` and
- `|i - j| <= k`

Otherwise, return `false`.

---

## **Example 1**

**Input:**

```python
nums = [1, 2, 3, 1], k = 3
```

**Output:**

```python
true
```

## **Example 2**

**Input:**

```python
nums = [1, 0, 1, 1], k = 1
```

**Output:**

```python
true
```

## **Example 3**

**Input:**

```python
nums = [1, 2, 3, 1, 2, 3], k = 2
```

**Output:**

```python
false
```

## Constraints:

- `1 <= nums.length <= 10⁵`
- `10⁹ <= nums[i] <= 10⁹`
- `0 <= k <= 10⁵`

## Approach & Algorithm

- This question required me to utilise the Sliding Window algorithm in order to solve it in an efficient manner. The question can be done using a brute force approach whereby we compare every single value in the array to the value in the given window, however this approach is not scalable and can be slow for large input sizes.
- Important thing to note is that `abs(i - j) <= k` means that our right pointer and left pointer values when subtracted will be less than or equal to the size of the window. SO in the example 1 above, the window size is actually 4 i.e., contains all 4 elements `[1, 2, 3, 1]` even though the size is `k = 3`. This is because `| 3 - 0 | == 3`, where the first `3` is the last index in the array and `0` is the first index. This means 4 values can be part of the window.
- I also have a set `window` that keeps track of this window. If we find a value that our `rightPtr` points to is part of our `window` set we return `True` as we have satisfied the condition `nums[i] == nums[j]`.
- In the solution below the line `if rightPtr - leftPtr > k:` just checks this condition essentially `abs(i - j) <= k` (inverted).
- Please view my whiteboard diagram for a visual representation.

## Code Implementation:

### Solution One (Sliding Window Algorithm):

- **Time Complexity:** O(n)

```python
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        window = set()
        leftPtr = 0

        for rightPtr in range(len(nums)):
            # We must first check to see if we have traversed past the window size.
            if rightPtr - leftPtr > k:
                # We must shift the window right by one.
                window.remove(nums[leftPtr])
                leftPtr += 1

            # We need to check to see if nums[rightPtr] is in the window.
            if nums[rightPtr] in window:
                return True

            window.add(nums[rightPtr])

        return False
```
