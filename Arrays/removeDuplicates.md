# Remove Duplicates from Array (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Remove Duplicates from Sorted Array**](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

---

## Problem Description

Given an integer array `nums` sorted in non-decreasing order, remove the duplicates **in-place** such that each unique element appears only once.  
The relative order of the elements should be kept the same.  
After removing the duplicates, return the number of unique elements.

### Constraints

- Modify the array in-place with O(1) extra space.
- The input array is sorted.

---

## Example

**Input**:  
`nums = [1, 1, 2]`

**Output**:  
`2, nums = [1, 2, _]`  
Explanation: `_` represents any value.

---

## Approach & Algorithms

### 1. Two Pointer Technique

1. I am using `i` and `j` as pointers. Pointer `j` keeps track of the unique element index (originally starts at index 1). NOTE: Index 0 is always unique.
2. I loop through the `nums` list as `i` is incremented. If the number stored at index `i` and `i - 1` differ it means a unique number has been encountered.
3. It means we can overwrite the number at index `j` with the number stored at index `i`.
4. We can continue till the loop finishes and we can return `j` as it represents the length of the 'updated list'.

### 2. In-Place Modification

- Use the same array for storing the result without allocating additional space.

---

## Code Solutions

### Solution 1: Two-Pointer (Slower)

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        # For performance reasons we can return if the list has length 0.
        if len(nums) == 0:
            return

        j = 1

        # Remember: First element is ALWAYS unique.
        for i in range(1, len(nums)):
            if nums[i] != nums[i - 1]:
                nums[j] = nums[i]
                j += 1

        return j
```

### Solution 2: Sorted Sets (Faster - Beats 100% of Solutions)

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        unique = sorted(set(nums))
        nums[:len(unique)] = unique
        return len(unique)
```
