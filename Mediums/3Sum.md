# 3Sum (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**15. 3Sum**](https://leetcode.com/problems/3sum/)

---

## **Problem Statement**

Given an integer array `nums`, return **all the triplets** `[nums[i], nums[j], nums[k]]` such that:

- `i != j`, `i != k`, and `j != k`
- `nums[i] + nums[j] + nums[k] == 0`

**Notice:** The solution **must not contain duplicate triplets**.

---

## **Example 1**

**Input:**
```python
nums = [-1,0,1,2,-1,-4]
```

**Output:**
```python
[[-1,-1,2],[-1,0,1]]
```

**Explanation:**
The valid triplets summing to `0` are:

- `(-1) + 0 + 1 = 0`
- `(-1) + (-1) + 2 = 0`

Only unique triplets are returned.

## **Example 2**

**Input:**
```python
nums = [0, 1, 1]
```

**Output:**
```python
[[]]
```

**Explanation:**
No valid triplets sum to `0`.

## **Example 3**

**Input:**
```python
nums = [0,0,0]
```

**Output:**
```python
[[0,0,0]]
```

**Explanation:**
The only valid triplet sums to `0`.

## Constraints

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 400`

---
## Approach & Algorithm

The **3Sum** problem is solved using the **two-pointer technique** after **sorting** the array. This reduces the time complexity to **O(N²)** instead of **O(N³)**.

- First, **sort `nums`** in **ascending order**.
- This makes it easier to use **two pointers** efficiently and avoid duplicate triplets.
- We iterate over `nums` with an **index `i`**.
- This element **acts as the first number** in our triplet.
- Initialize two pointers:
  - `leftPtr = i + 1` → Starts from the element **right after `i`**.
  - `rightPtr = n - 1` → Starts from the **end of `nums`**.
- These pointers help find **the two other numbers** that sum up to `0 - nums[i]`.
- Calculate the **current sum**:  
  ```python
  curSum = nums[i] + nums[leftPtr] + nums[rightPtr]
  ```
- If curSum == 0:
- Store `[nums[i], nums[leftPtr], nums[rightPtr]]` in the result.
- Move both pointers inward (`leftPtr++` and `rightPtr--`) to find the next unique triplet.
- Skip duplicate values for both `leftPtr` and `rightPtr` to avoid duplicate triplets.
- If `curSum > 0`, move `rightPtr` left (`rightPtr--`) to reduce the sum.
- If `curSum < 0`, move `leftPtr` right (`leftPtr++`) to increase the sum.
- Skipping duplicate `i` values in the outer loop avoids reprocessing the same triplets.
- Skipping duplicate `leftPtr` and `rightPtr` values ensures only unique triplets are added.

## Code Implementation

### Solution:

- **Time Complexity:** O(n^2)

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        n = len(nums)
        returnList = []
        target = 0

        for i in range(len(nums) - 2):
            # Skipping duplicates.
            if i > 0 and nums[i] == nums[i - 1]:
                continue

            leftPtr, rightPtr = i + 1, n - 1

            while leftPtr < rightPtr:
                curSumIter = nums[i] + nums[leftPtr] + nums[rightPtr]
                if curSumIter == target:
                    # We have found a list of nums that add up to 0 and are different
                    # i.e., i != j != k.
                    returnList.append([nums[i], nums[leftPtr], nums[rightPtr]])

                    # We must move our leftPtr forward and our rightPtr backward as this tuple already adds up to 0.
                    leftPtr += 1
                    while leftPtr < rightPtr and nums[leftPtr] == nums[leftPtr - 1]:
                        # We must ensure we skip any and all duplicates i.e., [-1, -1, -1, -1, 0, 1, 2]. It is important
                        # that we have the position 0, 1 and 6 in our array --> [-1, -1, 2] we don't want to have another -1
                        # of position 2, 3 or 4 again repeated. So we don't want [[-1, -1, 2], [-1, -1, 2], [-1, -1, 2]].
                        leftPtr += 1

                    # Do the same process for our rightPtr.
                    rightPtr -= 1
                    while leftPtr < rightPtr and nums[rightPtr] == nums[rightPtr + 1]:
                        rightPtr -= 1

                if curSumIter > target:
                    # We must move our rightPtr down.
                    rightPtr -= 1
                elif curSumIter < target:
                    # We must move up our leftPtr.
                    leftPtr += 1
        
        return returnList
```
