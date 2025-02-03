# Concatenate Array with Itself (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Concatenation of Array**](https://leetcode.com/problems/concatenation-of-array/description/)

---

## Problem Description

Given an integer array `nums` of length `n`, create an array `ans` of length `2n` such that:

- `ans[i] == nums[i]` for `0 <= i < n`.
- `ans[i + n] == nums[i]` for `0 <= i < n`.

Specifically, `ans` is the concatenation of two copies of `nums`.

Return the array `ans`.

---

## Examples

### **Example 1**

**Input:**  
`nums = [1, 2, 1]`

**Output:**  
`[1, 2, 1, 1, 2, 1]`

**Explanation:**

- `ans = [nums[0], nums[1], nums[2], nums[0], nums[1], nums[2]]`
- `ans = [1, 2, 1, 1, 2, 1]`

---

### **Example 2**

**Input:**  
`nums = [1, 3, 2, 1]`

**Output:**  
`[1, 3, 2, 1, 1, 3, 2, 1]`

**Explanation:**

- `ans = [nums[0], nums[1], nums[2], nums[3], nums[0], nums[1], nums[2], nums[3]]`
- `ans = [1, 3, 2, 1, 1, 3, 2, 1]`

---

## Constraints

- `n == nums.length`
- `1 <= n <= 1000`
- `1 <= nums[i] <= 1000`

---

## Approach & Algorithm

### 1. Duplicate Addition

- My first intuition in the solution below was to create a new separate dynamic array.
- I would then loop through the `nums` array and essentially copy it over to `new_nums` with each increment of `i`.
- I would also then copy over the number to position `i + len(nums)`.

### 2. Append

- My first solution above is not very fast as there may be times we need to insert into the middle of an array. This alone has a worst-case time complexity of `O(n)`.
- So, I thought what if we simply just append the numbers at the end of the array as appending to the end of an array is a constant-time (`O(1)`) operation.
- This method involves creating a `new_nums` array. We are then looping through twice the length of the `nums` array and appending elements to the back of the `new_nums` array.
- But the key here is that we are using the modulo operator to our advantage. So say we have an array `[1, 2]`, doing `append(nums[i % len(nums)])` where `i = 2`, evaluating this gives us `1 % 2 ==> 1`. So during the third iteration (`i = 2`) we simply append element at index 1 and get `[1, 2, 1]`. We can continue from there.

## Code Solutions

### Solution 1: Insertion Method (Not Fast)

- **Time Complexity**: It is `O(n^2)`.

```python
class Solution:
def getConcatenation(self, nums: List[int]) -> List[int]:
new_nums = []

for i in range(len(nums)):
    new_nums.insert(i, nums[i])
    new_nums.insert(i + len(nums), nums[i])

return new_nums
```

### Solution 2: Append Method (Faster)

- **Time Complexity**: It is `O(n)`.

```python
class Solution:
    def getConcatenation(self, nums: List[int]) -> List[int]:
        new_nums = []

        for i in range(2 * len(nums)):
            new_nums.append(nums[i % len(nums)])

        return new_nums
```
