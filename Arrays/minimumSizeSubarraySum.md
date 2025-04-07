# Minimum Size Subarray Sum (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**209. Minimum Size Subarray Sum**](https://leetcode.com/problems/minimum-size-subarray-sum/)

---

## **Problem Statement**

Given an array of **positive integers** `nums` and a **positive integer** `target`, return the **minimal length** of a subarray whose **sum is greater than or equal to `target`**.  
If there is no such subarray, return `0` instead.

---

## **Example 1**

**Input:**
```python
target = 7
nums = [2, 3, 1, 2, 4, 3]
```

**Output:**
`2`

**Explanation:**
The subarray `[4, 3]` has the minimal length with a sum ≥ 7.

## **Example 2**

**Input:**
```python
target = 4
nums = [1, 4, 4]
```

**Output:**
`1`

## **Example 3**

**Input:**
```python
target = 11
nums = [1, 1, 1, 1, 1, 1, 1, 1]
```

**Output:**
`0`

**Explanation:**
No subarray can be found with a sum ≥ 11.

---

## **Constraints**

- `1 <= target <= 10⁹`
- `1 <= nums.length <= 10⁵`
- `1 <= nums[i] <= 10⁴`

---

## Approach & Algorithm:

- I've utilised a sliding window algorithm (with variable window sizing).
- In essence we loop through the entire array of `nums`, and whilst looping we add the current value pointed to by our right pointer `R` to our `total` variable.
- Whilst looping we also need to check if the `total` is greater than or equal to the `target` that was passed in. If it was we must manually adjust the size of our window.
  - We must first however track the size of the window `length`. If the `length` is the same as the previous size of the window `length` from previous iterations we keep the `length` the same. However, if the current window is of size less than the current `length`, i.e., if `R - L + 1 < length` we have found a current window that is smaller and has a value equal to or greater than the target.
  - We dynamically add/subtract to our total whilst looping as using a `sum()` function each iteration would be costly. In our second loop we are moving the window so we must subtract the leftmost value i.e., `nums[L]` from our `total`. We then shift the left pointer `L` up.
- We then return the length of the window if it is less than the value orginally set (infinity).

## Code Implementation:

### Solution:

- **Time Complexity:** `O(n)`.

```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        total, L, length = 0, 0, float('inf')

        for R in range(len(nums)):
            total += nums[R]

            while total >= target:
                # We must find the length of current window prior to adjusting it.
                length = min(length, R - L + 1)
                total -= nums[L]

                # We need to adjust the size of the window by moving left pointer.
                L += 1
        
        return 0 if length == float('inf') else length
```