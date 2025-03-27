# Maximum Subarray (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**53. Maximum Subarray**](https://leetcode.com/problems/maximum-subarray/)

---

## **Problem Statement**

Given an integer array `nums`, find the **contiguous subarray (containing at least one number)** which has the **largest sum**, and return its sum.

---

## **Example 1**

**Input:**
```python
nums = [-2,1,-3,4,-1,2,1,-5,4]
```

**Output:**
```python
6
```

**Explanation:**

The subarray `[4, -1, 2, 1]` has the largest sum, which is `6`.

## **Example 2**

**Input:**
```python
nums = [1]
```

**Output:**
```python
1
```

**Explanation:**

The subarray `[1]` has the largest sum, which is `1`.

## **Example 3**

**Input:**
```python
nums = [5, 4, -1, 7, 8]
```

**Output:**
```python
23
```

**Explanation:**

The subarray `[5, 4, -1, 7, 8]` has the largest sum, which is `23`.

---

## **Constraints**

- The number of nodes in both trees is in the range `[0, 100]`
- `10⁴ <= Node.val <= 10⁴`

---

## Approach & Algorithm:

- I've utilised **Kadane's Algorithm** to solve this question in an efficient manner.
- In essence we have a window that slides/grows as we go through the array. If the `curSum` at any point is less than 0 we must reset it back to 0.
- Upon resetting this supposed window we need to grow it again. So we continue through the array and add to `curSum` the number stored at `nums[n]` index.
- Whilst looping through if at any point we see a `curSum` greater than `maxSum`, we essentially update the `maxSum` to the `curSum`.

## Code Implementation:

### Solution:

- **Time Complexity:** `O(n)` - We loop through the entire array.
- **Space Complexity:** `O(1)`

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        maxSum = nums[0]
        curSum = 0

        for n in range(len(nums)):
            curSum = max(curSum, 0)
            curSum += nums[n]
            maxSum = max(curSum, maxSum)
        
        return maxSum
```