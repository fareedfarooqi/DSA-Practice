# Maximum Sum Circular Subarray (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**918. Maximum Sum Circular Subarray**](https://leetcode.com/problems/maximum-sum-circular-subarray/)

---

## **Problem Statement**

Given a **circular integer array** `nums` of length `n`, return the **maximum possible sum** of a non-empty subarray of `nums`.

A **circular array** means the end of the array connects to the beginning of the array.  
Formally, the next element of `nums[i]` is `nums[(i + 1) % n]` and the previous element of `nums[i]` is `nums[(i - 1 + n) % n]`.

A subarray may only include each element of the fixed buffer `nums` at most once.  
Formally, for a subarray `nums[i], nums[i + 1], ..., nums[j]`, there does not exist `i <= k1, k2 <= j` with `k1 % n == k2 % n`.

---

## **Example 1**

**Input:**
```python
nums = [1, -2, 3, -2]
```

**Output:**
```python
3
```

**Explanation:**
- Subarray `[3]` has maximum sum `3`.

## **Example 2**

**Input:**
```python
nums = [5, -3, 5]
```

**Output:**
```python
10
```

**Explanation:**
- Subarray `[5, 5]` has maximum sum `5 + 5 = 10`.

## **Example 3**

**Input:**
```python
nums = [-3, -2, -3]
```

**Output:**
```python
-2
```

**Explanation:**
- Subarray `[-2]` has maximum sum `-2`.

---

## **Constraints**

- `n == nums.length`
- `1 <= n <= 3 * 10⁴`
- `3 * 10⁴ <= nums[i] <= 3 * 10⁴`

---

## Approach & Algorithm

- I have used a modified version of **Kadane's Algorithm** to solve this problem efficiently.
- The problem involves two main cases to consider:
  - Case 1: The maximum subarray is a **normal (non-circular) subarray**, meaning it lies somewhere completely inside the array without wrapping around. In this case, we can directly use the standard **Kadane's Algorithm** to find the maximum subarray sum.
  - Case 2: The maximum subarray is a **circular subarray**, meaning it wraps around the ends of the array (like `[HERE, NOT HERE, HERE]`). To find the sum in this case:
    - The **maximum circular subarray sum** is equivalent to the **total sum** of the array minus the **minimum subarray sum** (`total - globalMin`).
    - This is because, by removing the minimum subarray, we effectively select all other elements (the parts at the "ends") which will give us the circular maximum.
- The final result is the **maximum** between:
  - The standard maximum subarray sum (`globalMax`).
  - The circular maximum subarray sum (`total - globalMin`).
  - **NOTE:** An edge case exists whereby if all numbers in `nums` are negative we must simply return `globalMax` otherwise the algorithm will continue to run and return the minimum subarray.

## Code Implementation:

### Solution:

- **Time Complexity:** `O(n)` - We loop through the entire array.
- **Space Complexity:** `O(1)`

```python
class Solution:
    def maxSubarraySumCircular(self, nums: List[int]) -> int:
        curMax, curMin = 0, 0
        globalMax, globalMin = nums[0], nums[0]
        total = 0

        for n in nums:
            curMax = max(curMax + n, n)
            curMin = min(curMin + n, n)
            total += n
            globalMax = max(globalMax, curMax)
            globalMin = min(globalMin, curMin)

        return max(globalMax, total - globalMin) if globalMax > 0 else globalMax
```