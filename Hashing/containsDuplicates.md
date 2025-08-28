# Contains Duplicate (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Contains Duplicate**](https://leetcode.com/problems/contains-duplicate/)

---

## Problem Description:

Given an integer array `nums`, return **true** if any value appears **at least twice** in the array, and return **false** if every element is **distinct**.

---

## **Examples:**

### **Example 1**

**Input:**
```python
nums = [1,2,3,1]
```

**Output:**
```python
true
```

**Explanation:**
```plaintext
The element 1 occurs at the indices 0 and 3.
```

### **Example 2**

**Input:**
```python
nums = [1,2,3,4]
```

**Output:**
```python
false
```

**Explanation:**
```plaintext
All elements are distinct.
```

### **Example 3**

**Input:**
```python
nums = [1,1,1,3,3,4,3,2,4,2]
```

**Output:**
```python
true
```

## Constraints

- `1 <= nums.length <= 10^5`
- `10^9 <= nums[i] <= 10^9`

---

## Approach & Algorithm

- I have come up with two simple approaches:
  - We can utilise a `hashMap` or a `set` to solve this question.
- By definition sets cannot contain duplicates so we can create a `setNums` based off of `nums`. If the length of the `setNums` is less than the original `nums` we know that a duplicate is present and as such we can return `True`. If they are the same length than no duplicate is present and we can return `False`.
- We can also create a `HashMap`. By default hash maps cannot have duplicate keys. We can take this fact and create a `numsDict` (Hash Map) where the keys are based on the element in `nums`. We loop through `nums` to insert the key, if we find that the key exists in the `numsDict` already it means a duplicate is present and we can return `True`. Otherwise by the time we finish the loop and we haven't returned we know that no duplicates are present and we can return `False`.

## Code Implementation

### Solution 1 (Using Sets):

- **Time Complexity:** O(n)

```python

class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        setNums = set(nums)
        
        return True if len(setNums) < len(nums) else False


# More Pythonic Solution:

# class Solution:
    # def containsDuplicate(self, nums: List[int]) -> bool:
        # return not len(set(nums)) == len(nums)
```

### Solution 2 (Using Hash Maps):

- **Time Complexity:** O(n)

```python

class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        numsDict = {}

        for num in nums:
            if num in numsDict:
                return True
            else:
                numsDict[num] = 1
        
        return False

```
