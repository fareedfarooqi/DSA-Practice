# Two Sum (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Two Sum**](https://leetcode.com/problems/two-sum/)

---

## Problem Description

Given an array of integers `nums` and an integer `target`, return **indices** of the two numbers such that they add up to `target`.

- You may assume that **each input has exactly one solution**, and you **may not use the same element twice**.
- You can return the answer **in any order**.

---

## **Examples**

### **Example 1**

**Input:**
```python
nums = [2,7,11,15]
target = 9
```

**Output:**
```python
[0,1]
```

**Explanation:**
```plaintext
nums[0] + nums[1] == 9, so we return [0,1].
```

### **Example 2**

**Input:**
```python
nums = [3,2,4]
target = 6
```

**Output:**
```python
[1,2]
```

### **Example 3**

**Input:**
```python
nums = [3,3]
target = 6
```

**Output:**
```python
[0,1]
``` 

## Constraints

- `2 <= nums.length <= 10^4`
- `10^9 <= nums[i] <= 10^9`
- `10^9 <= target <= 10^9`
- Exactly one valid answer exists.

---

## Approach & Algorithm

- Solution 1 is slower. Please read it thoroughly for understanding.

## Code Implementation

### Solution 1 (Very Slow & Inefficient):

- **Time Complexity:** O(n^2)

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        numsDict = dict(enumerate(nums))
        
        for i in range(len(nums)):
            for key, value in numsDict.items():
                if i == key:
                    # We can skip as we can't have the solution include the number itself twice.
                    # So it CANNOT have the same index.
                    continue
                
                additionCheck = nums[i] + value

                if additionCheck == target:
                    return [i, key]
            

        return []
```

### Solution 2 (Faster & More Efficient):

- **Time Complexity:** O(n)

```python

```