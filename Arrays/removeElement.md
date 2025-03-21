# Remove Element from Array (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Remove Element**](https://leetcode.com/problems/remove-element/description/)

---

## Problem Description

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` **in-place**.  
The order of the elements may be changed.  
Then, return the number of elements in `nums` that are not equal to `val`.

### Requirements:

1. Modify the array in-place such that the first `k` elements contain only the elements that are not equal to `val`.
2. The remaining elements of `nums` beyond `k` are not important.
3. Return `k`, the number of elements in `nums` that are not equal to `val`.

### Custom Judge:

The judge will validate the solution with:

1. Ensuring `k` matches the length of the expected result.
2. Checking that the first `k` elements in `nums` match the expected result after sorting.
3. Ignoring the elements beyond index `k`.

---

## Example

### **Example 1**

**Input**:  
`nums = [3, 2, 2, 3]`, `val = 3`  
**Output**:  
`2, nums = [2, 2, _, _]`  
**Explanation**:

- Your function should return `k = 2`.
- The first two elements of `nums` should contain `2`.
- The remaining elements do not matter.

---

### **Example 2**

**Input**:  
`nums = [0, 1, 2, 2, 3, 0, 4, 2]`, `val = 2`  
**Output**:  
`5, nums = [0, 1, 4, 0, 3, _, _, _]`  
**Explanation**:

- Your function should return `k = 5`.
- The first five elements of `nums` contain `0, 1, 4, 0, and 3` (order can vary).
- The remaining elements do not matter.

---

## Constraints

- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`

---

## Approach & Algorithms

### 1. In-Place Removal

- So we are given a list of `nums` and we are required to remove all instances of `val`.
- We can do in-place removal whereby we can loop through the entire array and keep looping until we remove all instances of `val` from the array.

### 2. Two-Pointer Approach

- `i` scans through every element of the array.
- Whenever an element is NOT equal to `val` it is moved/copied to the index `j`, and `j` is incremented. So `j`is tracking `non-val` elements.
- After the loop the first `j` elements of `nums` are is the length of the modified array without `val`.

## Code Solutions

### Solution 1: Remove Method

- **Time Complexity**: It is `O(n^2)`.

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        while val in nums:
            nums.remove(val)
```

### Solution 2: Two-Pointer

- **Time Complexity**: It is `O(n)`.

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        # The 'j' variable will track our non-val index.
        j = 0

        # The 'i' variable will be used to scan the array.
        for i in range(len(nums)):
            if nums[i] != val:
                nums[j] = nums[i]
                j += 1

        return j
```
